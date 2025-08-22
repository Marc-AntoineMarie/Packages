Tu es un assistant capable de générer un site web moderne, responsive et interactif en HTML, CSS et JavaScript pur.  
Objectif : créer une landing page pour une société de gestion de patrimoine destinée aux jeunes, en s’inspirant de la structure et du style épuré du site cleerly.fr, mais en évitant toute copie directe.

Public cible : jeunes adultes (18-30 ans) souhaitant comprendre et optimiser leurs finances.

Style visuel :
- Palette moderne et lumineuse (bleu clair, turquoise, vert menthe)
- Typographie sans-serif moderne et lisible
- Sections avec fonds alternés (blanc / gris clair / dégradé léger)
- Icônes vectorielles simples et colorées
- Éléments avec coins arrondis, ombres douces et animations au survol
- Optimisé mobile et desktop

Structure demandée :
1. **Header** minimaliste avec logo (placeholder) et menu de navigation : Investir, Épargner, Retraite, Éducation, Blog
2. **Hero section** pleine largeur avec phrase d’accroche (“Construis ton avenir financier dès aujourd’hui”) + bouton d’appel à action (“Démarre ta simulation”)
3. **Bloc confiance** : 3 cartes mettant en avant les valeurs (Transparence, Simplicité, Accompagnement)
4. **Simulateur interactif** (JS pur) :
   - Demande âge, revenus mensuels, objectif (court / long terme)
   - Calcule et affiche instantanément un montant d’épargne conseillé
   - Résultat présenté dans une carte colorée avec un message motivant
5. **Section éducation** : 4 blocs avec icône + titre + court texte expliquant des concepts financiers de base (budget, épargne, investissement, retraite)
6. **Témoignages** : 2 ou 3 avis fictifs avec photo de profil circulaire et courte citation
7. **Blog / Articles** :
   - Afficher les articles dans une grille avec image, titre, résumé et bouton “Lire plus”
   - Ajouter un formulaire d’édition d’article accessible à un seul utilisateur (login simple en JS côté client)
   - L’utilisateur peut entrer un titre, une image (URL), un contenu, et l’article est ajouté dynamiquement au blog
   - Stockage temporaire en `localStorage` (pas de backend)
8. **Formulaire de contact** clair et simple : nom, email, message libre, bouton “Recevoir mon bilan gratuit”
9. **Footer** avec mentions légales, politique de confidentialité, liens réseaux sociaux

Fonctionnalités techniques :
- Simulateur 100 % côté client
- Effets hover sur boutons et cartes
- Animations douces (fade-in / slide-up) au chargement
- Blog géré côté client avec ajout d’articles en direct par un seul utilisateur
- Code clair, commenté, en un seul bloc (HTML + CSS + JS intégrés)

Contraintes :
- Ne pas copier de texte, image ou code de cleerly.fr
- Adapter le ton et le style pour un public jeune
- Donner directement le code complet prêt à être utilisé, sans explications hors du code
