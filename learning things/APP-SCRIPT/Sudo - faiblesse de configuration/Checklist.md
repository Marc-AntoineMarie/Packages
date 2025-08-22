# 1. Checklist spécifique : `app-script-ch1` → `app-script-ch1-cracked`

L’objectif est d’identifier **où tu peux exécuter du code avec les droits de `app-script-ch1-cracked`**.

### Étape 1 : Recherche de binaires setuid/setgid

Cherche tous les binaires qui tournent avec d’autres droits :

`find / -perm -4000 -type f 2>/dev/null find / -perm -2000 -type f 2>/dev/null`

- `-4000` = setuid
    
- `-2000` = setgid
    

Si tu vois un programme appartenant à `app-script-ch1-cracked` → bingo, c’est ton vecteur potentiel.

---

### Étape 2 : Vérifier `$PATH` hijacking

Certains programmes vulnérables utilisent `system("ls")` ou appellent un binaire sans chemin absolu.

- Vérifie les fichiers exécutables appartenant à `app-script-ch1-cracked`.
    
- Lance-les avec `strace` pour voir quelles commandes ils appellent :
    

`strace -f ./programme 2>&1 | grep exec`

---

### Étape 3 : Rechercher des fichiers modifiables

Est-ce que `app-script-ch1-cracked` exécute un script que tu peux modifier ?

`find / -user app-script-ch1-cracked -writable 2>/dev/null`

- Si oui → injection de commande.
    
- Pense aussi aux fichiers dans `/var/tmp`, `/tmp`, etc. qui pourraient être liés.
    

---

### Étape 4 : Cron jobs

Regarde si des tâches planifiées tournent sous `app-script-ch1-cracked` :

`cat /etc/crontab ls -l /etc/cron.*`

Si un script lancé par `app-script-ch1-cracked` est modifiable → tu peux injecter ton code.

---

### Étape 5 : Capabilities

Un binaire avec des capabilities spéciales peut t’ouvrir des portes :

`getcap -r / 2>/dev/null`

---

### Étape 6 : Vérifie l’environnement

- Variables d’environnement (`env`) → certains programmes héritent de ça.
    
- Vérifie aussi si tu peux exploiter un binaire avec `LD_PRELOAD` ou `LD_LIBRARY_PATH`.
    

---

### Étape 7 : Exploration ciblée

- Le dossier `notes/` pourrait contenir un indice (un script, une note, une consigne…).
    
- Tout ce qui appartient à `app-script-ch1-cracked` mérite ton attention.
    

---

# 2. Checklist globale (élévation de privilèges Linux)

Tu peux l’utiliser dans n’importe quel CTF / RootMe / pentest.

### Enumération initiale

- `id` → qui suis-je (user, groupe).
    
- `uname -a` → version du kernel.
    
- `lsb_release -a` ou `/etc/os-release` → version OS.
    
- `ps aux` → quels processus tournent.
    

---

### Fichiers et binaires

- `find / -perm -4000 -type f 2>/dev/null` → setuid root.
    
- `find / -perm -2000 -type f 2>/dev/null` → setgid.
    
- `ls -la /home /var /opt /tmp` → fichiers inhabituels.
    
- `getcap -r / 2>/dev/null` → capabilities.
    

---

### Config & sudo

- `sudo -l` → commandes possibles en sudo.
    
- `/etc/sudoers` → règles spéciales.
    

---

### Cron jobs

- `cat /etc/crontab`
    
- `ls -l /etc/cron.*`
    

---

### Services & process

- Ports ouverts : `netstat -tulnp`
    
- Process tournant avec privilèges élevés.
    
- Scripts de démarrage modifiables (`/etc/init.d`, systemd).
    

---

### Kernel & exploits

- Si vieux kernel → chercher un exploit kernel (DirtyCow, DirtyPipe…).
    

---

### Techniques avancées

- **LD_PRELOAD / LD_LIBRARY_PATH** : si un binaire setuid charge une lib, tu peux la détourner.
    
- **PATH hijacking** : si le binaire appelle un programme externe sans chemin absolu.
    
- **Buffer overflow / format string** : si binaire vulnérable.