# 1. Comprendre la vulnérabilité (niveau débutant)

Imagine que tu es invité à dîner. Le chef dit :

> "Va dans la cuisine et prends la casserole appelée `ls`".

Mais… dans la cuisine, il y a plusieurs casseroles avec des noms différents, et il prend **la première qu’il trouve** en fonction d’une liste d’endroits (c’est ton `$PATH`).

Si toi tu as réussi à placer **ta propre casserole appelée `ls`** au début de la liste, le chef va utiliser **ta casserole** au lieu de celle qu’il pensait.

C’est exactement ce qu’il se passe ici.

- Le programme (`ch11`) exécute la commande `ls …` sans préciser `/bin/ls`.
    
- Comme le programme est **setuid**, il s’exécute avec plus de privilèges que ton utilisateur.
    
- Donc, si tu fais en sorte que `ls` pointe vers **ton script**, c’est **ton code** qui s’exécute avec ces privilèges élevés.
    

---

# 2. Les briques techniques (niveau intermédiaire)

### a) `system()` en C

Dans le code du binaire on trouve :

`system("ls /challenge/app-script/ch11/.passwd");`

Que fait `system()` ?

- Il invoque `/bin/sh -c 'ls /challenge/app-script/ch11/.passwd'`.
    
- Donc, en réalité, c’est le shell qui cherche la commande `ls` en consultant la variable d’environnement **PATH**.
    

### b) La variable d’environnement PATH

`PATH` est une liste de répertoires séparés par `:`.  
Exemple :

`echo $PATH # /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin`

Quand tu tapes `ls`, le système regarde chaque répertoire dans l’ordre :

1. `/usr/local/sbin`
    
2. `/usr/local/bin`
    
3. `/usr/sbin`  
    …  
    jusqu’à trouver un fichier exécutable nommé `ls`.
    

Donc si tu mets ton propre dossier au **début** du PATH :

`export PATH=/tmp/pwn:$PATH`

alors `ls` sera trouvé dans `/tmp/pwn` avant `/bin/ls`.

### c) Les permissions SUID

Le binaire `./ch11` est **setuid**. Ça veut dire qu’il s’exécute avec les droits de son propriétaire (ici `app-script-ch11` ou parfois `root`), même si c’est toi qui le lances.

Concrètement :

- Normalement tu ne peux pas lire `$HOME/.passwd`.
    
- Mais si un programme setuid (qui a le droit de le lire) exécute ton code, tu gagnes cet accès.
    

### d) Exploitation

1. Créer un faux `ls` :
    
    `#!/bin/sh cat $HOME/.passwd`
    
2. Placer ce faux `ls` dans un dossier accessible.
    
3. Mettre ce dossier en tête du PATH.
    
4. Lancer le binaire → il exécute ton script au lieu du vrai `ls`.
    

---

# 3. Analyse sécurité (niveau avancé)

### Pourquoi c’est vulnérable ?

- Appeler `system("ls …")` au lieu de `/bin/ls …`
    
- Ne pas contrôler/assainir l’environnement (`PATH`, variables du shell)
    
- Être setuid **et** appeler un shell = combinaison très dangereuse.
    

### Comment l’attaquant pense ?

Un attaquant va se dire :

- "Est-ce que le binaire est setuid ?" → `ls -l ./ch11` montre `-rwsr-xr-x`.
    
- "Est-ce qu’il appelle `system()` ?" → `strings ./ch11 | grep system`
    
- "Utilise-t-il des commandes sans chemin absolu ?" → Bingo, `ls`.
    
- "Puis-je mettre un `ls` malveillant dans mon PATH ?" → Oui → exploitation.
    

### Comment se protéger ?

1. **Ne jamais** utiliser `system()` dans un programme setuid.
    
2. Si vraiment nécessaire → utiliser un chemin absolu (`/bin/ls`).
    
3. Mieux → remplacer par `execve("/bin/ls", args, clean_env)` en contrôlant tout.
    
4. Réinitialiser l’environnement avec `clearenv()` et reconstruire une version sûre.
    
5. En entreprise → activer des protections comme _capabilities_ Linux plutôt que setuid.
    

### Variantes d’exploitation

- On a vu ici **PATH hijacking**.
    
- Autres vecteurs possibles :
    
    - Injection via des variables comme `IFS`, `LD_PRELOAD` (si non protégé).
        
    - Exploiter le fait que le shell est `/bin/sh -c`, donc potentiellement `;` ou `&&` dans la commande si contrôlable.
        

### Exemple de faux `ls` plus agressif

`#!/bin/sh /bin/sh -p`

→ donne un shell avec les privilèges du binaire.

---

# Résumé du cours

- **Concept clé** : `system()` + setuid + commandes sans chemin absolu = vulnérabilité.
    
- **Exploitation** : détourner le PATH pour exécuter un faux binaire.
    
- **Impact** : accès à des fichiers protégés ou shell privilégié.
    
- **Prévention** : ne pas utiliser `system()`, utiliser des chemins absolus, nettoyer l’environnement.
    

---