# Renault_Internship
Stage de fin d'études chez Renault - Ampere Software Technologies (AST)

Maxence Maury

## Semaine 1 (23/03 -> 27/03)

Maxime Dandre, PO et tuteur de stage

Arrivée le lundi 23 mars.
Installation du poste, PC Windows et PC fixe Linux accessible en remote.
Beaucoup de demandes de droits.
Redéfinition plus précise du sujet de stage : Outil de tracking des exigences pour la traçabilité. 
Commencement du sujet de stage :
Premier MVP défini avec Maxime.
MVP : un tableau de bord web pour voir le pourcentage d'exigences (et autres indicateurs) testées dans le code. Code en Python.
Les exigences sont définies dans l'application Codebeamer. Les tests des exigences sont dans deux projets GitLab en Rust et Kotlin : DISCO et DriverUI (Software pour les écrans du tableau de bord des voitures Renault).
Avancement sur le MVP : itérations de POC et validation par Maxime.
- Mercredi 25 mars : premier POC fait en 3 jours, validé par Maxime : juste un dashboard sur des données mockées. Camembert de % d'exigences testées, liste des non testées.
- Lundi 30 mars : deuxième POC validé par Maxime : Dashboard plus complet basé sur un extract Codebeamer en Excel et sur les vrais repos Git des projets. Ajout de la gestion de dépôt Git et gestion de fichier Excel.

Suite du stage : Utiliser des LLMs pour l'automatisation de la vérification des tests et de l'éventuelle implémentation de ceux-ci.

## Semaine 2 (30/03 -> 03/04)
Formation opencode, et copilot. Renault cherche a utiliser l'IA de plus en plus et cherche des gens formé a l'IA.
fin de l'implem du dashboard MVP, dockerisation et exposition sur reseau interne a l'adresse du pc linux (qui tourne en permanance avec l'appli)
Mise en place petite CI locale pour valider qualité de code, sous forme de script. gitlab CI trop compliqué car pas de runner et projet privé (pas d'autres contributeurs) donc pas besoin.
Cleanup de l'appli et premier livrable au PO. Validé.
Mise en palce d'un vrai environnement de dev sur une autre branche avec un autre port d'exposition. jusqu'ici le dev servait de prod comme il n'y avait toujours pas de version stable.
cyber training et codebeamer training

## Semaine 3 (06/04 -> 10/04)
Finalisation de l'environnement de dev avec volumes docker de dev rajoutés dans le gitignore.
Presentation de moi a la reuninon de l'UET. participation a la reunion d'equipe avec le chef de service, Benoit, sur le future de l'equipe (problematiques de vision future et strategiques de renault et leurs impactes)
coté dev: avancé sur la parie IA.
Mise en place d'un RAG : 
- recuperation des tests dans le code en utilisant les mots clefs Rust et kotlin. On recupere le nom du test son header (commentaire) et le N premieres lignes de son implementation (pour eviter tests trop long)
- vectorisation des tests dans un FAISS avec faiss-cpu et sentence-transformers.
- recherche de similarité semantique par exigence : on recherche les K test les plus proches du id + nom + description de l'exigence.
- LLM: on demande a un LLM (ici LLm interne de renault gpt-4.1 car tokens gratuit) un score de confiance au fait que le test teste bien l'exigence.
Beaucoup de debug, d'apretissage, d'aide de LLM (license copilot interne utilisation principalement de claude opus 4.6).
Creation de template d'export codebeamer pour exporter les exigences. Revision du parsing excel du coup.
Reunion de suivi de stage avec tuteur pour presenter mes avencements et fixer les prochains objectifs.
Prochains objectifs: plus PO friendly et configurable pour possiblement une ouverture a d'autres projets/team. Donc configuration du model LLm en front rajout de logique metier pour comprehension, gain de temps et lisibilité.
Revision score IA, quelques ratés ... revoir comment ameliorer le RAG.

## Semaine 4 (20/04 -> 24/04)
Beaucoup de features sur l'appli de traçabilité (nommée reqtrack).

fiabilisation côté Excel, parsing de la description (beaucoup de CSS, etc.), review des boutons et de leurs fonctionnalités.
RAG séparé en deux étapes, plus un pipeline à proprement parler : d'abord le FAISS puis le LLM avec résultats intermédiaires.
feature : quand on a trouvé un test par IA, on peut maintenant automatiquement modifier le header et créer un commit,
future : partie push à revoir et ajouter le support multibranche.
Réunion avec Maxime en début de semaine pour valider les rendus et réajuster les nouvelles features, dont les commits et le RAG.
Deux matinées d'intégration stagiaires : rencontres de beaucoup d'autres stagiaires et perspectives de collaboration / présentation de nos sujets dans d'autres équipes.

copilot :
Cette semaine a surtout été consacrée à rendre reqtrack plus propre, plus robuste et plus proche d’un vrai outil utilisable en conditions réelles.
Gros travail sur l’architecture, notamment côté IA : séparation claire entre la partie FAISS (recherche sémantique) et la partie LLM (scoring et raisonnement). Ça a permis de mieux comprendre le pipeline RAG, de corriger plusieurs bugs et de préparer l’arrivée de plusieurs modèles LLM configurables via les endpoints backend.
La gestion des repositories Git a été nettement améliorée : sélection du repo depuis le front, ajout d’un bouton de pull, déplacement de la logique de refresh côté backend. L’index FAISS est maintenant reconstruit automatiquement quand les repos changent, ce qui garantit que l’IA travaille toujours sur un état cohérent du code.
Côté fonctionnalités, la partie génération de commits a bien évolué : commits conformes aux specs, avec possibilité d’éditer le message, le header et le nom de branche directement dans l’UI. Ça rend la feature beaucoup plus réaliste par rapport à un vrai workflow de dev.
Enfin, beaucoup de temps a été passé sur le nettoyage du code et l’UX : refactor du front pour du clean code, centralisation des messages d’erreur, correction des problèmes de sanitizing des descriptions, lint et format à répétition. L’objectif était clairement de passer d’un proto avancé à une base saine et maintenable.
En résumé : cette semaine marque une vraie montée en maturité du projet, avec des choix techniques plus clairs et une application plus stable, prête à être utilisée et étendue par la suite.

# Semaine 5 (27/04 -> 01/05)
J'ai fait de la maintenance sur reqtrack, j'ai fini d'ajouter des fonctionnalités esentiels comme le commit workflow, on peut commit et push depuis la page web reqtrack, j'ai optimisé le refresh four faire des taches en background pour que l'utilisation soit plus fluide.
J'ai principalement review toutes les fonctionnalités faites et si c'était bien fait.

copilot : 
Cette semaine, j’ai travaillé sur l’amélioration et la stabilisation de l’application, en corrigeant plusieurs bugs liés au routing, aux workflows Git et au parsing des commentaires.
J’ai également refactorisé le projet pour améliorer sa structure (séparation des routes, utilisation de constantes) et harmonisé le code grâce au linting et au formatage.
Par ailleurs, j’ai développé de nouvelles fonctionnalités autour de la gestion des exigences : ajout d’un champ "status", mise à jour du parser Excel pour gérer ce champ, et création d’un composant "AllRequirements" intégré au dashboard.
Enfin, j’ai amélioré la robustesse globale de l’application en optimisant la gestion des erreurs et certains traitements en arrière-plan.

# Semaine 6 (04/05 -> 08/05) -- CURRENT
