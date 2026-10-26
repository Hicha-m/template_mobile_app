# Langages et approches pour créer une app mobile

Statut : guide de choix initial. Aucune stack n’est encore retenue pour le dépôt.

## 1. Distinguer langage et framework

Un **langage** sert à écrire le code : TypeScript, Dart, Kotlin, Swift ou C#.

Un **framework** fournit les outils et composants pour construire l’app : React Native, Flutter ou .NET MAUI. Expo fournit un ensemble d’outils et de services autour de React Native.

Le choix porte donc sur une combinaison : langage, framework, plateformes, bibliothèques et chaîne de compilation. Un même langage ne permet pas automatiquement de partager toute l’interface entre iOS et Android.

## 2. Principales possibilités

| Approche | Langage(s) | Technologies courantes | Plateformes et partage | Quand la choisir | Points d’attention |
| --- | --- | --- | --- | --- | --- |
| Multiplateforme avec React Native | TypeScript ou JavaScript | React Native, Expo | iOS et Android ; grande partie du code partagée | Compétences React/web ; app de contenu, service, commerce ou outil métier | Interface différente du HTML/CSS du navigateur ; certains besoins nécessitent du code natif ou une compilation adaptée |
| Multiplateforme avec Flutter | Dart | Flutter | iOS et Android ; UI et logique largement partagées | Interface personnalisée et cohérente ; volonté d’adopter un environnement commun | Apprentissage de Dart et des widgets ; accès aux fonctions natives selon les plugins ou du code spécifique |
| Android natif | Kotlin ; Java possible | Jetpack Compose pour Kotlin ; vues Android pour Kotlin/Java | Android ; code de l’app spécifique à cette plateforme | Android prioritaire, intégration système poussée | Une app iOS complète exige une autre implémentation ; Kotlin est généralement privilégié pour un nouveau projet |
| iOS natif | Swift ; Objective-C possible | SwiftUI, UIKit | iOS ; code de l’app spécifique à cette plateforme | iPhone/iPad prioritaires, intégration poussée à l’écosystème Apple | Android demande une autre implémentation ; Objective-C concerne surtout du code existant |
| Partage de logique avec Kotlin Multiplatform | Kotlin ; Swift pour une UI iOS native | Kotlin Multiplatform, éventuellement Compose Multiplatform | Logique partagée entre Android et iOS ; UI native séparée ou UI partagée selon l’approche | Partager le métier et les données tout en gardant le choix de l’interface | Architecture et intégrations à évaluer ; préciser ce qui est réellement partagé et testé |
| Multiplateforme .NET | C# ; XAML possible pour décrire l’UI | .NET MAUI | Android et iOS ; grande partie du code partagée | Équipe déjà à l’aise avec C#/.NET, notamment pour des outils métier | Écosystème, bibliothèques et comportement par plateforme à vérifier pour les besoins du projet |
| App web embarquée | TypeScript ou JavaScript, HTML et CSS | Ionic avec Capacitor ; Capacitor avec un framework web | Interface web dans une app iOS/Android ; accès natif via plugins | Réutiliser une app web ou des compétences web, interfaces surtout fondées sur des formulaires et contenus | Tester fluidité, clavier, accessibilité et disponibilité des plugins ; respecter les exigences des stores |
| App web installable | TypeScript ou JavaScript, HTML et CSS | PWA avec le framework web de son choix | Navigateur, installation selon le système ; déploiement web | Valider rapidement une idée, distribuer par URL, besoins compatibles avec le web | Capacités et comportement variables selon navigateur/OS ; distribution et fonctions différentes d’une app de store |

**Multiplateforme ne signifie pas absence de travail par plateforme.** Permissions, clavier, navigation, achats, notifications, builds et tests doivent être vérifiés séparément.

## 3. Langages pour des besoins spécialisés

| Langage | Usage pertinent | Limite pour ce dépôt |
| --- | --- | --- |
| C++ | Moteurs de jeux, calcul, traitement de médias et bibliothèques natives partagées | Complexité élevée pour une app classique ; interface et intégration restent à construire |
| Rust | Bibliothèque métier ou calcul partagé, intégrée au mobile par des interfaces natives | Outillage d’intégration supplémentaire ; aucun starter généraliste prévu au départ |
| C# avec Unity | Jeux et expériences interactives utilisant un moteur de jeu | À traiter dans une catégorie dédiée ; une app métier classique utilise d’autres composants |
| GDScript ou C# avec Godot | Jeux 2D/3D | Vérifier le support d’export mobile de la version et du langage choisis ; hors starter applicatif initial |
| Python | Scripts, automatisation, backend ; apps possibles avec Kivy ou BeeWare | Évaluer packaging, bibliothèques natives, maintenance et expérience mobile avant de le retenir pour une app distribuée |

Ces possibilités peuvent être référencées dans le catalogue sans engagement à maintenir un starter pour chacune.

## 4. Le backend est un choix distinct

Une app mobile peut appeler une API écrite en TypeScript/JavaScript, Python, Go, Java, Kotlin, C#, PHP, Ruby ou un autre langage adapté. Elle n’a pas besoin d’utiliser le même langage que le serveur.

Le choix du backend dépend des données, de l’hébergement, des compétences, du coût et des services nécessaires. Une app locale peut ne pas avoir de backend. Les clés privées et traitements nécessitant un secret restent côté serveur.

## 5. Comment choisir

| Situation | Options à examiner en priorité |
| --- | --- |
| Je connais React et TypeScript et je vise iOS + Android | React Native avec Expo |
| Je veux un environnement commun et une UI très personnalisée | Flutter avec Dart |
| Je vise Android uniquement | Kotlin avec Jetpack Compose |
| Je vise iOS uniquement | Swift avec SwiftUI, UIKit selon les besoins |
| Je veux partager la logique avec des interfaces natives | Kotlin Multiplatform |
| Je maîtrise déjà C#/.NET | .NET MAUI |
| Je veux réutiliser une interface web existante | Capacitor, éventuellement avec Ionic |
| Je veux d’abord tester une idée via un lien | PWA, si les capacités web suffisent |

Ce tableau oriente l’évaluation ; il ne remplace pas un essai sur les fonctions critiques.

Avant de choisir, préciser :
- plateformes et versions minimales ;
- compétences et disponibilité de l’équipe ;
- besoins natifs : caméra, Bluetooth, tâches en arrière-plan, achats, etc. ;
- contraintes d’interface, accessibilité et performances ;
- dépendances indispensables, maintenance, licences et coûts ;
- accès aux appareils, outils de build et comptes de distribution.

Pour les approches listées, la compilation locale iOS passe par la chaîne Apple, généralement sur macOS avec Xcode. Certains services permettent des builds distants ; ils ne dispensent pas des tests iOS ni des exigences de signature et de distribution applicables.

## 6. Conséquences pour template_mobile_app

Le catalogue peut couvrir plusieurs langages, mais chaque ressource doit être étiquetée avec sa stack. Un composant Flutter n’est pas directement réutilisable dans React Native.

Éléments partageables entre stacks :
- modèles de recherche, cadrage produit et tests utilisateurs ;
- parcours, principes de design, spécifications et assets dont la licence le permet ;
- contrats API, scénarios de validation et checklists de publication, avec variantes par plateforme.

Éléments à implémenter ou adapter par stack :
- composants UI et navigation ;
- gestion d’état, stockage et accès aux fonctions natives ;
- configuration, builds et tests automatisés.

La première version avec code doit retenir **une stack de référence**. Les autres pourront d’abord apparaître comme ressources documentées, puis recevoir des exemples si des besoins réels et une capacité de maintenance le justifient.

**Recommandation initiale conditionnelle :** si l’objectif principal est d’aller plus vite en venant du web et en connaissant React/TypeScript, commencer l’évaluation par TypeScript + React Native + Expo. Comparer avec Flutter si l’équipe préfère adopter Dart et son système de widgets. Aucun de ces choix n’est arrêté à ce stade.
