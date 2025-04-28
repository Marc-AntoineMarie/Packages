# Cahier des charges détaillé – Plateforme Telora

## 1. Contexte et Présentation générale

Telora est une application web de gestion de contacts, d’annuaires téléphoniques et d’utilisateurs, pensée pour un fonctionnement en marque blanche. Elle vise à permettre à différents types d’utilisateurs (Admins, Partenaires, Clients finaux) de gérer leurs propres données, via une interface moderne, responsive et sécurisée.  
Le projet est développé en PHP/MySQL côté serveur, avec une interface HTML/CSS/JS enrichie par TailwindCSS et FontAwesome.

## 2. Objectifs principaux

- Centraliser la gestion des contacts et des utilisateurs pour des clients variés (partenaires, entreprises, utilisateurs finaux).
- Offrir une séparation stricte des accès selon le rôle.
- Proposer une expérience utilisateur fluide, moderne et sécurisée.
- Permettre l’import/export de contacts au format CSV, avec robustesse face aux erreurs de format.

## 3. Public cible

- Administrateurs système (super-admins)
- Partenaires (entreprises clientes de Telora)
- Clients finaux (utilisateurs des partenaires)

## 4. Expression des besoins et fonctionnalités

### 4.1. Gestion multi-niveaux et rôles

- **Admins** : gestion globale des partenaires, clients, utilisateurs, et contacts.
- **Partenaires** : gestion de leurs propres clients finaux et de leurs contacts.
- **Clients finaux** : gestion de leurs propres contacts et informations.

### 4.2. Gestion des entités

- CRUD complet (création, lecture, modification, suppression) pour :
    - Clients
    - Utilisateurs
    - Contacts de l’annuaire
- Import/export CSV des contacts (encodage UTF-8, format compatible)
- Recherche, filtrage, pagination des contacts

### 4.3. Sécurité et navigation

- Séparation stricte des accès selon le rôle (aucune fuite de données entre clients)
- Gestion du contexte de navigation via la session PHP
- Redirection automatique vers la page de connexion en cas d’accès non autorisé
- Logs d’erreur activés pour le suivi des bugs (sans fuite d’informations sensibles)
- Jamais de modification des variables de session à partir de l’URL côté client
- Vérification stricte des droits d’accès à chaque page sensible

### 4.4. Interface utilisateur

- Interface responsive, moderne, centrée, avec header harmonisé sur toutes les pages
- Utilisation de containers pour centrer et limiter la largeur du contenu (max 1200px)
- Design cohérent entre tous les formulaires et tableaux
- Utilisation de boutons modernes, feedback utilisateur (succès/erreur), modals pour les actions sensibles
- Intégration de TailwindCSS et FontAwesome

### 4.5. Points d’attention

- Maintien du contexte utilisateur lors de la navigation (pas de fuite de session)
- Cohérence visuelle et UX sur toutes les pages (header, boutons, tableaux, formulaires)
- Robustesse de la gestion des imports/exports CSV (gestion des erreurs de format)
- Tests sur différents rôles et scénarios d’accès

## 5. Contraintes techniques

- **Technologies** : PHP (backend), MySQL (base de données), HTML/CSS/JS (frontend), TailwindCSS, FontAwesome
- **Organisation** : séparation claire entre la logique métier (PHP, dossier classes/api), les vues (HTML, dossiers admin, annuaire, clientlist, utilisateurdetail…), et le style (CSS, partials)
- **Sécurité** : sessions PHP, contrôle d’accès, logs d’erreur, protection contre la modification des sessions côté client
- **Ergonomie** : centrage du contenu, largeur limitée, responsive design
- **Tests** : activation des logs, rédaction d’un cahier de tests fonctionnels, tests manuels/automatisés selon disponibilité

## 6. Architecture technique (modules/dossiers)

- **admin/** : gestion des administrateurs et des partenaires
- **annuaire/** : gestion des contacts et de l’annuaire téléphonique
- **clientlist/** et **clientdetail/** : gestion des clients
- **utilisateurdetail/** : gestion des utilisateurs
- **api/** : endpoints pour l’interface ou l’intégration externe
- **classes/** : logique métier et objets PHP
- **config/**, **database/** : configuration et scripts SQL
- **login/** : authentification et gestion des sessions
- **partials/** : fragments d’interface (header, footer…)
- **utils/** : utilitaires divers
- **docs/**, **Documentation_LDAP/** : documentation technique et d’intégration

## 7. Livrables attendus

- Code source complet (PHP, CSS, JS, SQL)
- Documentation technique (structure, installation, sécurité)
- Cahier de tests fonctionnels (scénarios d’accès, sécurité, import/export)
- Fichiers d’exemple pour l’import/export CSV

## 8. Déploiement et maintenance

- Déploiement sur un serveur compatible PHP/MySQL, avec configuration sécurisée (HTTPS recommandé)
- Scripts d’installation et de migration de base de données fournis
- Procédures de sauvegarde et de restauration des données à documenter

## 9. Sécurité et RGPD

- Protection des données personnelles (sessions, accès, logs limités)
- Conformité RGPD à assurer (mentions légales, droits des utilisateurs)
- Certificat SSL recommandé pour toutes les communications

## 10. Tests et validation

- Rédaction d’un cahier de tests couvrant tous les rôles et scénarios critiques
- Tests d’import/export CSV avec gestion des erreurs
- Validation finale par démonstration auprès du tuteur