# 1. Contexte : la GOT et la PLT

Quand un programme C appelle une fonction de bibliothèque (par ex. `printf`), l’adresse réelle de cette fonction n’est pas connue au moment de la compilation.  
Le binaire contient alors une **table d’adresses dynamiques** appelée :

- **GOT (Global Offset Table)** : table en mémoire qui contient les adresses des fonctions importées.
    
- **PLT (Procedure Linkage Table)** : une sorte de trampoline qui passe par la GOT pour aller chercher l’adresse réelle.
    

En gros :

`Ton code -> PLT -> GOT -> vraie adresse (dans libc par ex.)`

Au premier appel, l’éditeur de liens dynamique (ld-linux.so) résout l’adresse, la met dans la GOT, et ensuite toutes les prochaines fois, ça passe direct.

---

# 2. L’exploitation possible sans RELRO

Un attaquant peut essayer de **réécrire une entrée dans la GOT** (par un overflow, par exemple).  
Exemple classique : remplacer l’adresse de `printf` par `system`.  
→ À chaque fois que le programme appellera `printf`, en réalité ce sera `system` qui sera exécuté.

C’est ce que montre ton code de test :

`unsigned int *p = (void*)(strtol(argv[1], NULL, 0)); *p = (unsigned int)fake_printf;`

Ici, tu forces l’écriture à une adresse précise (`argv[1]`), et tu mets `fake_printf` à la place de `printf`.

Sans protection → ça marche, on a bien le message _GOT overwriten !_

---

# 3. RELRO : Relocation Read-Only

RELRO est une option de compilation **qui rend la GOT en lecture seule après la résolution des symboles dynamiques**.  
Il existe deux niveaux :

- **Partial RELRO** (`-Wl,-z,relro`) :  
    Seule une partie des sections sensibles est protégée. Mais les entrées de la GOT utilisées par le PLT restent modifiables. Donc encore exploitable.
    
- **Full RELRO** (`-Wl,-z,relro,-z,now`) :  
    Le linker résout **toutes** les fonctions dynamiques dès le démarrage du programme (option `now`), puis **verrouille la GOT en lecture seule**.  
    → Impossible de la modifier par un exploit : tentative d’écriture = **segmentation fault**.
    

---

# 4. Ton test, décortiqué

Sans RELRO :

`$ gcc test.c $ readelf -r ./a.out | grep printf 08049790  R_386_JUMP_SLOT   printf $ ./a.out 0x08049790 GOT overwriten !`

- La GOT contient une entrée modifiable pour `printf`.
    
- Tu l’écrases, et quand le programme appelle `printf`, c’est `fake_printf` qui est appelé.
    

Avec Full RELRO :

`$ gcc test.c -Wl,-z,relro,-z,now $ readelf -r ./a.out | grep printf 08049fe8  R_386_JUMP_SLOT   printf $ ./a.out 0x08049fe8 Erreur de segmentation`

- Ici, la GOT est en mémoire **lecture seule**.
    
- Quand tu essaies d’écrire à `0x08049fe8`, le CPU génère une faute de segmentation → crash.
    
- Donc plus possible de détourner l’exécution en modifiant la GOT.
    

---

# 5. Résumé clair

- **But de RELRO** : empêcher la réécriture de la GOT.
    
- **Partial RELRO** : un peu de protection mais GOT toujours modifiable.
    
- **Full RELRO** : GOT figée → empêche les attaques de type GOT overwrite.
    
- **Conséquence pour un attaquant** : il faut trouver d’autres techniques (ROP, ret2libc, etc.), car l’overwrite GOT est bloqué.
    

---

# 6. Exemple concret d’exploitation évitée

Sans RELRO :

`printf(user_input);`

Si tu peux écraser l’entrée GOT de `printf` → tu mets `system`.  
Ensuite tu envoies `"/bin/sh"` comme entrée → tu as un shell.

Avec Full RELRO :  
Impossible, car GOT non modifiable.

---

👉 En clair : **RELRO est une des protections "modernes" compilateur/linker** pour durcir les binaires et empêcher une technique d’exploitation bien connue (GOT overwrite). Mais ça n’empêche pas d’autres attaques (buffer overflow avec ROP, etc.).