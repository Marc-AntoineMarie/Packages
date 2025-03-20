## Prérequis

Avant de commencer, assurez-vous d'avoir les informations suivantes :

- Type de poste (ex: "Yealink T54")
- Numéro d'extension
- Adresse MAC
- Numéro de série
- Adresse IP du serveur SIP
- SIP login du poste
- SIP password du poste

## Étapes

1. **Réinitialisation du téléphone**  
	    Assurez-vous que le téléphone est en configuration usine. Si ce n'est pas le cas, effectuez une réinitialisation aux paramètres d'usine.
    
2. **Création d'un nouvel utilisateur dans LDAP**
    
    - Ouvrez le logiciel LDAP.
        
    - Accédez à la catégorie _Administration d'un client_.
        
    - Cliquez sur _Nouveau_ pour créer un utilisateur.
        
    - Remplissez les champs avec les informations collectées préalablement.
        
    - Créez les BLF si nécessaire.
        
    - Vous pouvez également utiliser le bouton _autoBLF_ pour importer automatiquement tous les utilisateurs existants.
        
3. **Configuration de l'autoprovisioning**
    
    - Accédez à l'interface web du téléphone concerné.
        
    - Ajoutez le lien suivant :  
        `http://54.36.189.50/Autoprov/`
        
    - Validez la configuration.
        

Votre téléphone est maintenant configuré et prêt à l'emploi.