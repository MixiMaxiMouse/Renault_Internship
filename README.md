# Renault_Internship
Stage de fin d'études chez Renault - Ampere Software Technologies (AST)

Maxence Maury

## Semaine 1

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

## Semaine 2 
Formation opencode, et copilot. Renault cherche a utiliser l'IA de plus en plus et cherche des gens formé a l'IA.
fin de l'implem du dashboard MVP, dockerisation et exposition sur reseau interne a l'adresse du pc linux (qui tourne en permanance avec l'appli)
Mise en place petite CI locale pour valider qualité de code, sous forme de script. gitlab CI trop compliqué car pas de runner et projet privé (pas d'autres contributeurs) donc pas besoin.
Cleanup de l'appli et premier livrable au PO. Validé.
Mise en palce d'un vrai environnement de dev sur une autre branche avec un autre port d'exposition. jusqu'ici le dev servait de prod comme il n'y avait toujours pas de version stable.
cyber training et codebeamer training

## Semaine 3
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

