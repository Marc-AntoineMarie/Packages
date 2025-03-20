# Guide d'utilisation de Feedly pour une veille PHP/Laravel optimisée

## Introduction

Feedly est un agrégateur de flux RSS puissant qui permet de centraliser et d'organiser efficacement votre veille technologique. Ce guide vous explique comment configurer et optimiser Feedly spécifiquement pour suivre l'écosystème PHP et Laravel.

## 1. Organisation de votre veille PHP/Laravel

### Création d'une structure de collections

Dans Feedly, organisez vos sources en collections thématiques :

1. Cliquez sur "+" à côté de "Collections" dans le menu latéral
2. Créez les collections suivantes :

```
- PHP Core
  • Actualités officielles PHP
  • Blogs techniques PHP
  • Sécurité PHP
  
- Laravel Ecosystem
  • Laravel officiel
  • Packages Laravel
  • Tutoriels Laravel
  
- PHP/Laravel Community
  • Forums et discussions
  • Conférences
  • Influenceurs

- PHP/Laravel Tools
  • Outils de développement
  • DevOps PHP
  • Performances
```

### Configuration des flux prioritaires

1. Pour chaque source importante, cliquez sur les trois points (...)
2. Sélectionnez "Marquer comme prioritaire"
3. Sources à marquer en priorité :
   - Site officiel de PHP
   - Laravel News
   - Annonces de sécurité PHP/Laravel

## 2. Ajout des sources essentielles

### Sources PHP (à ajouter dans la collection "PHP Core")

Recherchez et ajoutez ces sources dans Feedly :

- **PHP.net feed** : `https://www.php.net/feed.atom`
- **PHP Releases** : `https://www.php.net/releases/feed.php`
- **PHP Annotated Monthly** : `https://blog.jetbrains.com/phpstorm/category/php-annotated-monthly/feed/`
- **Stitcher.io** : `https://stitcher.io/rss`
- **PHP Builder** : `https://www.phpbuilder.com/rss/feed.php`
- **PHP Security** : `https://www.php.net/security/feed.php`

### Sources Laravel (à ajouter dans la collection "Laravel Ecosystem")

- **Laravel News** : `https://feed.laravel-news.com/`
- **Laravel Blog** : `https://blog.laravel.com/feed`
- **Taylor Otwell** : `https://medium.com/feed/@taylorotwell`
- **Freek Van der Herten** : `https://freek.dev/feed`
- **Spatie Blog** : `https://spatie.be/feed`
- **Laravel Daily** : `https://laraveldaily.com/feed`

### Sources communautaires (à ajouter dans "PHP/Laravel Community")

- **Reddit r/PHP** : `https://www.reddit.com/r/PHP/.rss`
- **Reddit r/Laravel** : `https://www.reddit.com/r/laravel/.rss`
- **PHP Roundtable** : `https://www.phproundtable.com/feed.xml`
- **Laravel.io** : `https://laravel.io/feed`

### Sources outils et écosystème (à ajouter dans "PHP/Laravel Tools")

- **Packagist** : `https://packagist.org/feeds/releases.rss`
- **PHP The Right Way** : `https://www.phptherightway.com/feed.xml`
- **Laravel Ecosystem** : `https://postsrc.com/feeds/laravel-ecosystem`

## 3. Techniques d'optimisation de la veille sur Feedly

### Filtrage efficace

1. Utilisez la fonction "Power Search" (version Pro) ou la recherche standard :
   - Recherchez des termes comme "PHP 8.3", "Laravel 11", "security"
   - Sauvegardez ces recherches pour un accès rapide

2. Créez des filtres personnalisés (version Pro) :
   - Filtre "Sécurité" : articles contenant "security", "vulnerability", "CVE"
   - Filtre "Nouveautés" : articles contenant "release", "new feature", "update"

### Utilisation des tags

1. Créez des tags pertinents pour votre veille :
   - `#àlire` : articles à approfondir plus tard
   - `#important` : mises à jour cruciales
   - `#idée` : inspirations pour projets futurs
   - `#sécurité` : alertes et bonnes pratiques

2. Pour taguer un article :
   - Survolez l'article
   - Cliquez sur l'icône d'étiquette
   - Sélectionnez ou créez un tag

### Organisation de la lecture

1. Utilisez la fonction "Enregistrer pour plus tard" :
   - Cliquez sur l'icône de signet sur les articles
   - Consultez-les dans la section "À lire plus tard"

2. Établissez une routine de lecture :
   - **Traitement quotidien** (15 min) : parcourir les titres, marquer les articles importants
   - **Lecture approfondie** (30-45 min, 2 fois par semaine) : lire les articles sauvegardés

## 4. Intégration avec d'autres outils

### Exportation vers des outils de prise de notes

1. **Notion** :
   - Installez l'extension de navigateur Notion
   - Lors de la lecture d'un article, cliquez sur l'extension pour l'enregistrer
   - Organisez dans une base de données Notion dédiée à votre veille

2. **Obsidian** :
   - Utilisez la fonction "Email to save" de Feedly Pro
   - Configurez un service comme IFTTT pour transférer ces emails vers un dossier
   - Importez les contenus dans Obsidian

### Automatisation avec IFTTT/Zapier

1. **Configuration IFTTT** :
   - Créez un compte sur [IFTTT](https://ifttt.com/)
   - Connectez votre compte Feedly
   - Créez des applets comme :
     - "Envoyer les articles taggés #important vers Slack"
     - "Créer une note dans Notion pour chaque article sauvegardé"

2. **Configuration Zapier** (alternative plus puissante) :
   - Créez des zaps pour envoyer des articles spécifiques vers :
     - Trello (pour organiser des tâches liées)
     - Google Sheets (pour créer une base de données de ressources)
     - Slack (pour partager avec votre équipe)

## 5. Workflow recommandé pour une veille efficace

### Routine quotidienne (15 minutes)

1. Ouvrez Feedly et consultez la section "Aujourd'hui"
2. Parcourez rapidement les titres en mode "Vue titre"
3. Pour chaque article pertinent :
   - Sauvegardez-le (icône signet) pour lecture approfondie
   - Ou lisez-le immédiatement s'il est court/urgent
   - Appliquez un tag approprié (#important, #àlire, etc.)
4. Vérifiez spécifiquement les sources prioritaires

### Session bi-hebdomadaire (30-45 minutes)

1. Ouvrez la section "À lire plus tard"
2. Lisez les articles sauvegardés
3. Pour chaque article important :
   - Prenez des notes concises
   - Exportez vers Notion/Obsidian/autre outil
   - Supprimez de la liste "À lire plus tard" une fois traité

### Révision mensuelle (60 minutes)

1. Évaluez la pertinence de vos sources actuelles
2. Ajoutez de nouvelles sources découvertes durant le mois
3. Supprimez les sources peu utiles ou trop bruyantes
4. Affinez vos tags et filtres
5. Créez une synthèse mensuelle des points clés à retenir

## 6. Astuces spécifiques pour PHP/Laravel

### Mots-clés à surveiller

Configurez des recherches sauvegardées pour ces termes :

- **PHP** : "PHP 8.3", "PHP 8.4", "JIT", "PHP RFC", "PHP attributes"
- **Laravel** : "Laravel 11", "Livewire", "Folio", "Octane", "Breeze", "Jetstream"
- **Sécurité** : "PHP security", "Laravel security", "composer security"
- **Performance** : "PHP performance", "Laravel optimization", "database optimization"

### Identification des articles à forte valeur

Priorisez les articles qui :
- Expliquent les nouvelles fonctionnalités avec des exemples concrets
- Partagent des benchmarks ou comparaisons
- Proposent des solutions à des problèmes courants
- Présentent des patterns de conception

### Évaluation des sources

Pour chaque source, évaluez périodiquement :
- **Ratio signal/bruit** : pourcentage d'articles pertinents
- **Fraîcheur** : fréquence de publication
- **Profondeur** : qualité du contenu technique
- **Applicabilité** : utilité pratique pour vos projets

## Conclusion

Feedly, correctement configuré, est un outil puissant pour centraliser et optimiser votre veille technologique sur PHP et Laravel. Cette méthodologie vous permettra de rester informé des évolutions importantes tout en limitant le temps consacré à cette veille. L'automatisation et l'organisation sont les clés pour transformer cette veille en connaissance actionnable dans vos projets.

N'hésitez pas à adapter ce système à vos besoins spécifiques et à l'affiner progressivement pour qu'il corresponde parfaitement à votre façon de travailler.
