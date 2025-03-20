Ce guide présente les méthodes pour exécuter automatiquement un script Perl en tant que processus daemon au démarrage d'un système Linux.

## Méthode 1 : Configuration avec systemd (recommandée)

systemd est le système d'initialisation standard sur la plupart des distributions Linux modernes. Cette méthode offre une gestion complète du cycle de vie de votre processus.

### Étapes de configuration :

1. **Créer un fichier de service systemd**
    
    ```bash
    sudo nano /etc/systemd/system/mon-script-perl.service
    ```
    
2. **Ajouter la configuration suivante**
    
    ```
    [Unit]
    Description=Mon script Perl
    After=network.target
    
    [Service]
    Type=simple
    ExecStart=/usr/bin/perl /chemin/vers/votre/script.pl
    User=utilisateur
    Group=groupe
    Restart=on-failure
    
    [Install]
    WantedBy=multi-user.target
    ```
    
    Remplacez :
    
    - `/chemin/vers/votre/script.pl` par le chemin absolu de votre script
    - `utilisateur` et `groupe` par l'utilisateur et le groupe sous lesquels le script doit s'exécuter
3. **Activer et démarrer le service**
    
    ```bash
    sudo systemctl enable mon-script-perl.service
    sudo systemctl start mon-script-perl.service
    ```
    
4. **Vérifier l'état du service**
    
    ```bash
    sudo systemctl status mon-script-perl.service
    ```
    

### Configuration avancée pour une haute disponibilité

Pour garantir que votre script tourne en permanence, même en cas d'erreur :

```
[Service]
...
Restart=always
RestartSec=5
```

Cela forcera systemd à redémarrer votre script quelles que soient les conditions d'arrêt, avec un délai de 5 secondes entre les tentatives.

### Avantages de systemd

- Gestion des dépendances système
- Journalisation automatique (`journalctl -u mon-script-perl.service`)
- Surveillance de l'état du processus
- Redémarrage automatique en cas d'échec
- Gestion des permissions d'exécution

## Méthode 2 : Utilisation de crontab avec @reboot

Une alternative plus simple mais moins robuste.

1. **Ouvrir crontab en édition**
    
    ```bash
    crontab -e
    ```
    
2. **Ajouter la ligne suivante**
    
    ```
    @reboot /usr/bin/perl /chemin/vers/votre/script.pl
    ```
    

## Vérification des permissions

Quelle que soit la méthode choisie, assurez-vous que votre script a les permissions d'exécution :

```bash
chmod +x /chemin/vers/votre/script.pl
```

## Dépannage

- **Le script ne démarre pas** : Vérifiez les journaux avec `journalctl -u mon-script-perl.service`
- **Erreurs de permission** : Vérifiez les droits d'accès aux fichiers et répertoires
- **Dépendances manquantes** : Assurez-vous que toutes les bibliothèques Perl nécessaires sont installées