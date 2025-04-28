**Plateforme Telora**  

## *1. Présentation générale*

Telora est une application web de gestion de contacts, d’annuaires téléphoniques et d’utilisateurs, pensée pour un fonctionnement en marque blanche. Elle permet à différents types d’utilisateurs (Admins, Partenaires, Clients finaux) de gérer leurs propres données, avec une interface moderne, responsive et sécurisée.

---

## *2. Objectifs fonctionnels*

### *2.1. Gestion multi-niveaux*

**Admins** : Super-administrateurs, gèrent tous les partenaires et clients.  
**Partenaires** : Entreprises clientes de Telora, gèrent uniquement leurs propres clients finaux.  
**Clients** : Utilisateurs finaux, accèdent uniquement à leurs propres données.  

### *2.2. Gestion des clients et utilisateurs*

Listing, création, modification, suppression de clients (par les Admins et Partenaires).  
Listing, création, modification, suppression d’utilisateurs (par Partenaires et Clients selon droits).  

### *2.3. Gestion de l’annuaire téléphonique*

CRUD sur les contacts de l’annuaire pour chaque client.  
Import/export CSV des contacts (encodage UTF-8, format compatible).  
Recherche, filtrage, pagination des contacts.  

### *2.4. Sécurité & navigation*

Séparation stricte des accès selon le rôle (un client ne peut jamais voir les données d’un autre).  
Contrôle du contexte de navigation (partenaire/client) via la session.  
Redirection automatique vers la page de connexion en cas d’accès non autorisé.  

### *2.5. Interface utilisateur*

Interface responsive, moderne, centrée, avec header harmonisé sur toutes les pages.  
Utilisation de containers pour centrer et limiter la largeur du contenu.  
Design cohérent entre tous les formulaires et tableaux.  
Utilisation de boutons modernes, feedback utilisateur (succès/erreur), modals pour les actions sensibles.

---

  

## *3. Contraintes techniques*

**Technologies** : PHP (backend), MySQL (base de données), HTML/CSS/JS (frontend), TailwindCSS et FontAwesome pour le style.  
**Organisation** : Séparation claire entre la logique métier (PHP), les vues (HTML), et le style (CSS).  
**Sécurité** :  
Sessions PHP pour l’authentification et la gestion du contexte.  
Jamais de modification des variables de session à partir de l’URL côté client.  
Vérification stricte des droits d’accès à chaque page sensible.  
**Ergonomie** :  
Centrage du contenu principal.  
Largeur limitée à 1200px pour la lisibilité.  
Responsive design pour tous les écrans.  
**Logs & Debug** : Activation des logs d’erreur pour le suivi des bugs (sans fuite d’informations sensibles).

---

  

## *4. Points d’attention*

Maintien du contexte utilisateur lors de la navigation (pas de fuite de session).  
Cohérence visuelle et UX sur toutes les pages (header, boutons, tableaux, formulaires).  
Tests sur différents rôles et scénarios d’accès.  
Gestion des imports/exports CSV : robustesse face aux erreurs de format.

---

  

## *5. Livrables attendus*

Code source complet (PHP, CSS, JS, SQL).  
Documentation technique (structure, installation, sécurité).  
Cahier de tests fonctionnels (scénarios d’accès, sécurité, import/export).  
Fichiers d’exemple pour l’import/export CSV.