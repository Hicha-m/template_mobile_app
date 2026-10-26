# Cahier des charges — template_mobile_app

Version : 0.1 — 26 octobre 2026  
Statut : proposition de cadrage ; aucune implémentation à ce stade.

## 1. Objectif

Réduire le temps nécessaire pour démarrer et livrer une application mobile iOS et Android en regroupant des ressources sélectionnées, des recettes d’intégration, des composants réutilisables et des projets de départ.

Le dépôt doit permettre de partir d’un besoin (« ajouter une connexion », « afficher une liste hors ligne », « publier sur les stores »), de choisir une solution adaptée et de l’intégrer sans reconstruire les mêmes fondations.

Public visé : développeurs indépendants et petites équipes, notamment habitués au développement web.

## 2. Positionnement et périmètre

Le dépôt évoluera en trois couches :

1. **Catalogue Awesome** : bibliothèques, outils et documentations classés par besoin, avec recommandations motivées et limites.
2. **Recettes et composants** : exemples minimaux, code réutilisable et instructions d’intégration.
3. **Starters** : projets cohérents assemblant les éléments validés, avec application de démonstration.

La première livraison porte sur la documentation et la définition des sections. Les ressources, composants et starters décrits ci-dessous sont des livrables futurs.

Principes :
- réutiliser les bibliothèques maintenues avant d’écrire une abstraction ;
- privilégier une solution recommandée par besoin et expliquer quand choisir une alternative ;
- distinguer composants visuels, modules fonctionnels et services externes ;
- permettre de prendre un élément sans embarquer tout le dépôt ;
- documenter les écarts entre iOS et Android ;
- garder les services payants et les fonctions métier facultatifs.

Hors périmètre initial : créer un nouveau framework, maintenir plusieurs implémentations équivalentes, construire un backend universel ou couvrir tous les métiers.

## 3. Choix techniques à arbitrer

Aucun framework n’est imposé par ce document.

| Décision | Critères de choix | Moment |
| --- | --- | --- |
| Stack de référence : React Native/Expo, Flutter ou natif | Compétences, vitesse de démarrage, accès aux API natives, maintenance | Avant les premiers composants |
| Plateformes et versions minimales | Public cible, appareils disponibles, compatibilité des dépendances | Avant le starter |
| Backend et authentification | Besoin de serveur, hébergement, coût, export des données | Avant le module de connexion |
| Distribution du code | Copie documentée, paquet ou template ; simplicité de mise à jour | Avant la première livraison de code |
| Licence du dépôt | Réutilisation commerciale, attribution, compatibilité des dépendances | Avant la diffusion de composants |

Recommandation de méthode : retenir une seule stack pour le premier starter. Le catalogue peut présenter d’autres écosystèmes, en indiquant clairement leur compatibilité. Évaluer React Native avec Expo en priorité si la continuité avec JavaScript/TypeScript est un objectif ; cette recommandation reste à valider.

## 4. Sections du catalogue

Priorités : **P0** = nécessaire au premier socle utilisable ; **P1** = extension courante ; **P2** = besoin avancé ou spécialisé. Ces niveaux concernent la future réalisation, pas le contenu déjà disponible.

| Section | Besoins couverts et éléments réutilisables | Exigence de validation | Priorité |
| --- | --- | --- | --- |
| 01 — Démarrage et environnement | Prérequis, installation, émulateurs, appareil réel, configuration, dépannage | Un développeur suit les commandes depuis un environnement propre ; contraintes macOS/Xcode pour iOS explicites | P0 |
| 02 — Architecture et configuration | Arborescence, modules par fonctionnalité, variables publiques, environnements, conventions | Ajouter une fonctionnalité sans dépendance circulaire ; aucun secret serveur dans l’app | P0 |
| 03 — Design system et composants UI | Couleurs, typographie, espacements, icônes, boutons, champs, cartes, listes, modales, bottom sheets | Thèmes clair/sombre, états désactivé/chargement/erreur, personnalisation sans modifier le composant | P0 |
| 04 — Navigation et liens | Piles, onglets, parcours protégés, retour Android, liens profonds et liens universels | Retour cohérent, ouverture d’une route depuis un lien et redirection après connexion | P0 |
| 05 — Écrans et parcours prêts à adapter | Accueil, liste/détail, profil, paramètres, onboarding, connexion, erreur | Chaque écran gère chargement, absence de données et erreur ; données de démonstration identifiées | P0 |
| 06 — Formulaires et validation | Champs, sélection, dates, messages, validation locale et serveur | Clavier adapté, focus visible, défilement du champ actif, prévention des doubles envois | P0 |
| 07 — Authentification et compte | Inscription, connexion, récupération, session, déconnexion, suppression de compte | Session expirée traitée ; jetons stockés de façon adaptée ; contrôle d’accès effectué côté serveur | P0 |
| 08 — API et état applicatif | Client réseau, cache, pagination, annulation, erreurs, séparation état local/distant | Délais dépassés et échecs récupérables ; erreurs compréhensibles ; absence de requêtes inutiles | P0 |
| 09 — Stockage et mode hors ligne | Préférences, stockage sécurisé, base locale, cache, file de synchronisation | Redémarrage sans perte indue ; comportement hors ligne explicite ; conflits documentés | P0 pour stockage/cache ; P1 pour synchronisation |
| 10 — Permissions et cycle de vie | Caméra, photos, localisation, demandes contextuelles, arrière-plan/premier plan | Refus et révocation gérés ; retour depuis les réglages ; conservation de l’état utile | P0 pour le socle ; P1 pour les intégrations |
| 11 — Médias et fichiers | Capture, galerie, documents, compression, téléversement, lecture audio/vidéo | Fichier volumineux, annulation, reprise ou nouvel essai ; limites de formats et tailles documentées | P1 |
| 12 — Notifications | Notifications locales et push, préférences, routage, renouvellement des jetons | Permission refusée ; ouverture au premier plan, en arrière-plan et app arrêtée | P1 |
| 13 — Recherche et exploration | Recherche, filtres, tri, listes longues, favoris | Saisie rapide, résultat vide, pagination et conservation des filtres | P1 |
| 14 — Capacités natives | Géolocalisation, cartes, biométrie, partage, contacts, haptique ; Bluetooth/NFC selon besoin | Support par plateforme, permissions, appareil requis et limites d’arrière-plan explicités | P1 ; Bluetooth/NFC P2 |
| 15 — Paiement et abonnements | Achats intégrés, restauration, droits d’accès, paiement de biens/services | Distinguer biens numériques et physiques ; sandbox ; droits vérifiés côté serveur | P2 |
| 16 — Internationalisation et accessibilité | Traductions, pluriels, dates, RTL, lecteur d’écran, taille du texte, mouvement réduit | Parcours principal accessible ; texte agrandi sans blocage ; absence de chaînes critiques codées en dur | P0 |
| 17 — Sécurité et confidentialité | Stockage sensible, journaux expurgés, suppression/export, permissions minimales | Aucun secret embarqué ; données sensibles absentes des logs ; collecte et conservation documentées | P0 |
| 18 — Qualité et tests | Analyse statique, tests unitaires utiles, intégration, parcours de bout en bout, matrice appareils | Installation, parcours principal, erreur réseau et reprise de session vérifiés sur iOS et Android | P0 |
| 19 — Performance et diagnostic | Démarrage, listes, images, mémoire, crashs, logs, suivi d’erreurs | Mesures sur build de production et appareil de référence ; budget défini avant optimisation | P1 ; diagnostic de base P0 |
| 20 — Build et publication | Identifiants, signature, CI, builds, distribution interne, stores, versions et mises à jour | Build reproductible ; secrets de signature hors dépôt ; procédure de publication et reprise documentée | P0 |
| 21 — Services et fonctions métier | Analytics avec consentement si requis, feature flags, chat, temps réel, OCR/IA | Service remplaçable ; coût et données transmises visibles ; panne du service gérée | P2 |
| 22 — Maintenance et contribution | Versions supportées, mises à jour, licences, dépréciation, proposition de ressources | Chaque entrée possède un statut et une date de vérification ; procédure de remplacement | P0 |

## 5. Format obligatoire d’une ressource

Chaque entrée du catalogue contient :
- nom, lien officiel et problème résolu ;
- catégorie : bibliothèque, service, composant, recette ou starter ;
- stack et plateformes compatibles, versions vérifiées ;
- raison du choix et cas où une alternative convient mieux ;
- licence du code ; tarif ou limites gratuites pour un service ;
- dépendances, permissions et compte externe éventuellement requis ;
- difficulté d’intégration : simple, intermédiaire ou avancée, avec justification ;
- statut : à évaluer, évalué, intégré, déprécié ;
- date et périmètre de la dernière vérification.

Une entrée ne reçoit pas le statut « intégré » sur la seule base de sa documentation : elle doit avoir été utilisée dans un exemple reproductible. La présence dans le catalogue ne vaut pas validation pour tous les usages.

## 6. Contrat d’un composant ou module réutilisable

Chaque élément livré avec du code doit fournir :
1. Un objectif limité et une interface publique documentée : paramètres, retours et événements.
2. Les prérequis, versions, dépendances et étapes d’installation.
3. Un exemple minimal exécutable et une démonstration dans l’app dédiée.
4. Les options de thème et de traduction si l’élément affiche du texte ou une interface.
5. Les états applicables : chargement, vide, succès, erreur, désactivation et absence de réseau.
6. Les différences iOS/Android, permissions et besoins de compilation native.
7. Les limites connues, tests pertinents et instructions de mise à jour.
8. L’origine du code et une licence compatible avec sa réutilisation.

Les modules dépendant d’un backend doivent expliciter le contrat API et fournir des données simulées identifiées comme telles. Les identifiants de démonstration ne doivent pas devenir des identifiants de production.

## 7. Organisation cible du dépôt

Arborescence indicative, à créer progressivement au moment des livraisons :

```text
README.md
docs/
  cahier-des-charges.md
  choix-techniques.md
  demarrage.md
  publication.md
catalogue/
  01-demarrage.md
  02-architecture.md
  ... une fiche par section
recipes/
  ... recettes d’intégration
components/
  ... composants UI de la stack retenue
modules/
  ... blocs fonctionnels
starters/
  ... projets de départ
examples/
  ... application de démonstration
templates/
  fiche-ressource.md
  fiche-composant.md
CONTRIBUTING.md
```

Le README servira de point d’entrée : objectif, accès par besoin, niveau de maturité, stack supportée, démarrage et contribution. Les dossiers de code ne seront créés que lorsqu’ils contiendront un élément utilisable.

## 8. Première version utilisable envisagée

Parcours démonstrateur : démarrer l’app, consulter une liste et un détail, saisir un formulaire, se connecter, modifier ses préférences et retrouver les données mises en cache sans réseau.

Contenu recommandé :
- un starter iOS/Android avec une stack de référence ;
- navigation, thème, traductions et configuration d’environnement ;
- boutons, champs, cartes, états vide/erreur/chargement et modale ;
- écrans liste/détail, connexion, profil et paramètres ;
- client API, gestion d’erreurs, cache local et stockage sécurisé ;
- un parcours d’authentification complet avec un fournisseur choisi ;
- instructions pour lancer, tester et produire un build de distribution interne.

Les données simulées permettent de lancer la démonstration sans service externe. La recette d’authentification réelle doit préciser séparément sa configuration et sa validation.

## 9. Critères d’acceptation

### Livraison documentaire actuelle
- Les grandes étapes d’une app mobile, du démarrage à la maintenance, sont couvertes.
- Chaque section décrit les éléments attendus, sa priorité et une condition de validation.
- Le catalogue, les composants et les starters ont des rôles distincts.
- Les choix encore ouverts et les futurs livrables sont explicitement identifiés.

### Future première version avec code
- Une personne peut créer un projet à partir du starter en suivant uniquement la documentation.
- Les versions des outils et commandes de lancement sont indiquées.
- Le parcours démonstrateur fonctionne sur iOS et Android ; appareils et versions testés sont consignés.
- Clavier, zones sûres, retour Android, permissions refusées, perte de réseau et expiration de session sont traités.
- Un composant peut être réutilisé dans un projet distinct sans dépendre de l’app de démonstration.
- Aucun secret ni donnée personnelle réelle ne figure dans les exemples.
- Une distribution interne peut être produite depuis la procédure documentée.

Objectif initial à mesurer : obtenir un premier écran sur un appareil ou un simulateur en moins de 30 minutes, une fois les outils système installés. Ce délai est une cible, pas une promesse validée.

## 10. Feuille de route

| Étape | Livrables | Condition de passage |
| --- | --- | --- |
| A — Cadrage | Ce cahier des charges, priorités, choix techniques à décider | Périmètre et stack de référence retenus avant le code |
| B — Catalogue initial | Fiches P0, critères de sélection, guide de contribution | Recommandations documentées ; statuts honnêtes ; liens vérifiés |
| C — Socle | Starter, navigation, thème, UI, configuration et démonstration | Démarrage reproductible sur les deux plateformes |
| D — Parcours complet | API, formulaires, compte, stockage et erreurs | Parcours démonstrateur et cas d’échec vérifiés |
| E — Livraison | Tests utiles, CI, builds internes et guide stores | Distribution interne reproductible |
| F — Extensions | Modules P1 puis P2 selon les besoins réels | Chaque ajout répond à un cas d’usage et respecte le contrat |

Aucune durée n’est fixée avant le choix de la stack et l’évaluation des intégrations.

## 11. Maintenance et mesure du bénéfice

Suivre le temps jusqu’au premier lancement, le temps d’intégration d’un module, les problèmes rencontrés lors de la réutilisation et les incompatibilités découvertes après mise à jour.

Avant chaque livraison, vérifier les dépendances, les liens, les licences, les commandes et les plateformes annoncées. Toute modification incompatible doit être accompagnée d’un guide de migration. Les entrées obsolètes doivent être signalées ou retirées avec une solution de remplacement quand elle existe.

Le succès du dépôt se mesure à la réutilisation effective de ses éléments dans de nouvelles apps.
