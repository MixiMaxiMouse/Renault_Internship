# Renault_Internship
Stage de fin d'études chez Renault - Ampere Software Technologies (AST)

Maxence Maury

## Glossaire
FAISS = Facebook AI Similarity Search \
ReqTrack = l'app que je develope, Requirement Tracking \
Maxime DANDRE = PO et tuteur entreprise

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
J’ai continué à développer et améliorer l’application de traçabilité que j'ai nommé ReqTrack en ajoutant plusieurs fonctionnalités importantes. J’ai travaillé sur la fiabilisation du parsing Excel, ainsi que sur le traitement des descriptions (notamment avec du CSS), tout en revoyant les boutons et leur comportement pour assurer une meilleure cohérence globale.
Côté IA, j’ai clarifié le fonctionnement du RAG en le séparant en deux étapes distinctes : une première basée sur FAISS pour la recherche, puis une seconde avec le LLM, ce qui permet d’avoir des résultats intermédiaires plus exploitables et un fonctionnement plus propre. J’ai aussi ajouté une fonctionnalité permettant, après identification d’un test par l’IA, de modifier automatiquement le header et de générer un commit.
En parallèle, j’ai continué à améliorer la gestion Git (avec encore des évolutions prévues, notamment sur le push et le multi-branches) et à nettoyer le code pour le rendre plus maintenable. Une réunion avec mon encadrant en début de semaine m’a permis de valider les choix réalisés et d’ajuster certaines features, notamment autour des commits et du RAG.
Enfin, j’ai participé à deux matinées d’intégration avec d’autres stagiaires, ce qui a permis d’échanger sur les projets et d’envisager des collaborations avec d’autres équipes.

## Semaine 5 (27/04 -> 01/05)
J’ai travaillé sur la maintenance de ReqTrack en consolidant les fonctionnalités existantes, notamment en finalisant le système de commit et de push directement depuis l’interface web. J’ai également optimisé le rafraîchissement de l’application en passant certains traitements en arrière-plan comme le build de l'index du FAISS(Facebook AI Similarity Search) afin de rendre l’utilisation plus fluide.
En parallèle, j’ai revu l’ensemble des fonctionnalités déjà développées pour vérifier leur bon fonctionnement et leur qualité. Cela m’a aussi amené à corriger plusieurs bugs (routing, workflows Git, parsing) et à améliorer la structure du code via du refactoring et du nettoyage. Enfin, j’ai continué à faire évoluer l’application en ajoutant des éléments comme la gestion du statut des exigences et son intégration dans le dashboard.

## Semaine 6 (04/05 -> 08/05)
Livraison de reqtrack v3 a Maxime (la version avec RAG) feedback tres positif avec quelques bug fix durant la review avec lui.
Puis concentration sur le ticket jira de converstion de tests unitaires en test composants en Kotlin sur l'appli DriverUI (affichage tableau de bord centrale), et sur l'outil CLI de reqtrack type headless batch.
pour le ticket jira: aussi vu la mise a jour automatique des headers au bon format avec agent skill et MCP server (Model Context Protocol).

## Semaine 7 (11/05 -> 13/05)
Travail sur l'outil CLI reqtrack. refacto de l'app reqtrack de layer architecture vers layer + core engine. utilisation du core engine pour le CLI: 
1/ OUTIL crée
lister tous les SCRS
identifier les manquants
pour les manquants, identifier des présents sémantiquement (hint seuil minimal à déterminer)
2/ IA (prompt/script/commande à rédiger)
vérification de l'état réel ds le code
présent en unit test?
hint confirmé ou infirmé
réellement manquant
production d'un rapport + stratégie d'implémentation pour limiter à 500 lignes le nb de modif potentiel (toujours plusieurs MR vs plusieurs commits)
3/ IA/DEV 
ingestion de l'implementation part x
réalisation du code
review

step 1 réalisé avec nouvel endpoint qui genere un rapport en json et appel http a l'endpoint dans le script, script lancé directement depuis docker.
step 2 au debut je voulais faire un script qui n'utilise pas http ou d'endpoint et qui accédait directement au core engine depuis le docker mais au final :
plus propre de faire un script en dehors du docker et qui aura acces a un orchestrateur d'agents comme opencode pour les etapes 2 et 3.
De plus comme j'ai opté pour un appel http a un endpoint je n'ai plus besoin d'executer le script dans le meme environnement docker. par contre il faut que le docker tourne.
Pour le moment probleme de taille entre le nombre de tokens que le llm prends et la taille de ma requete, (trop de requirements). meme avec un gros modele comme claude sonnet 4.6.


copilot competence :
Au regard des éléments présentés, ton niveau sur la compétence « Réaliser des solutions numériques » peut être argumenté au niveau Maîtrise. En effet, tu ne te contentes pas de produire une solution fonctionnelle : tu as conçu et fait évoluer un outil complet (ReqTrack) en prenant en compte l’ensemble du cycle de développement, depuis la définition d’un MVP jusqu’à des versions avancées intégrant de l’IA (RAG avec FAISS + LLM), la conteneurisation Docker et une exposition réseau. Tes choix techniques sont justifiés et adaptés à ton environnement (absence de GitLab CI → mise en place d’une CI locale, utilisation d’un LLM interne pour des contraintes de coûts, séparation du pipeline RAG pour améliorer lisibilité et exploitabilité), ce qui montre une capacité à composer avec des contraintes réelles. Tu démontres également une vision systémique et évolutive : refactorisation vers une architecture core engine + layers, création d’un CLI headless pour industrialisation, réflexion sur la scalabilité (problème de tokens LLM, limitation des modifications à 500 lignes, stratégie de MR), et ouverture vers des orchestrateurs d’agents. L’intégration de bonnes pratiques (dockerisation, refactoring, gestion des branches, qualité de code, sécurité via environnement interne) ainsi que la collaboration avec ton PO (itérations régulières, feedback, validation) illustrent une démarche professionnelle complète et structurée. Enfin, tu analyses les limites de ta solution (fiabilité du RAG, erreurs de scoring IA, contraintes de volumétrie) et proposes des axes d’amélioration et de repli, ce qui montre une capacité à anticiper l’impact et l’adaptabilité de ta solution dans différents contextes. L’ensemble de ces éléments correspond clairement au niveau maîtrise, avec des solutions à la fois avancées, cohérentes, adaptatives et en interaction avec leur environnement technique et organisationnel.

## Semaine 8 (18/05 -> 22/05)
Création d'une pipeline d'agents IA pour conversion de test unitaire en test composant en kotlin. un agent orchestrateur qui a 2 sous agents un mcp et des skills.
sous agents de strategie des test et de review. l'orchestrateur ensuite modifie les test identifié en utilisant un mcp qui donne acces a des outils de build et test du l'app et des skills de classification de type de tests, de detection de documentation d'exigence, de conversion de test et de validation de test
donc mise en place de l'environement gradle et android studio pour build l'app Driver UI en kotlin. création d'un MCP qui expose les outils runw build, test, lint, check ...

## Semaine 9 (26/05 -> 29/05)
Ajout de test android au lieu de conversion de unitaire vers android car impossible au final de convertif. trop d'ecart de logique. Donc rework de l'agent, création des premiers test, et surtout installation de cuttlefish et l'environnement de dev android pour lancer les tests android.
pour les rest unitaires il faut juste ./runw test mais pour les composants / android il faut l'app android qui tourne sur un emulateur. Ici cuttlefish qui a besoin de Kvm et quemu. apres il faut build l'apk de l'appli et le push sur le cuttlefish. puis on peut run les tests avec ./gradlew connectedDebugAndroidTest.
Beaucou de réunion PIP = Project Increment Planning. on voit ce que l'equipe va faire sur du long terme (2027-28) et on s'engage sur les 3 prochains sprints de 3 semaines. 
Beaucoup de probleme de proxy dns environnement renault...


## Semaine 10 (01/06 -> 05/06)
Finalisation de convertions de tests unitaires en tests composant (en kotlin android tests car on test des @Composable). création d'un agent de conversion de test non fructueuse. L'agent se base trop sur les test unitaires et va dans toutes directions. meilleur par iteration sans agent. 
Les tests doivent couvrir les exigences (ici software requirement : SCRS) qui sont deja couvert par des tests unitaires mais la QA ne prend en compte que la tracabilité des tests android.
Les test manquants sont principalement sur deux composants: Odometer et Autonomy widget.
Au debut j'ai rajouté des fichiers de tests en suivant les test conventions donc utiliser la coroutine tryEmit au lieu de runTest comme dans les autres fichiers legacy.
Mais probleme de coherence et trop de fichiers de test pour des composants pas si gros.
les tests android actuels n'etaient plus a jour avec les test conventions du projet. 
J'ai donc réecrit les tests dans un seul fichier au lieu de plusieurs avec chacun un setup (avant setup partagé par class abstraite mais illisible).
j'ai uniformisé le niveau de mock, avant: une fois mocké a la couche presentation une fois application une fois infra ... Maintenant: mock couche infra donc on test bien les couches application et presentation.
Donc reformattage des tests et rajout de tests.
MR en attente de review.

## Semaine 11 (08/06 -> 12/06) -- CURRENT
Retour sur le sujet reqtrack tracabilité des exigences avec outils CLI en headless pour rectifier les scrs non tracés par batch et plus unitairement.
Benchmark de l'outil/skill IA graphify qui est censé créer un graph du projet pour permettre au llm de naviguer plus rapidement et efficacement dans le projet en economisant des tokens.
premiere version du CLI : 
- on crée un endpoint /analyze qui cree un fichier json avec : tous les scrs séparés en deux listes par testés et non testés.
- chaque scrs a son id nom description etc. Chaque scrs testé a le path du fichier qui le test, et chaque non testé a une liste de 5 candidat de similarité sémentique choisi avec FAISS.
- on donne ce compte rendu a un agent IA qui a pour role de review les scrs et trouver ceux qui pourraient etre rajoutés (en rajoutant son nom dans le header d'un test qui le testerai deja)
- on crée un rapport de changement via ce premier agent puis on apelle un deuxieme agent qui aura pour but d'implementer ces changements par bloc de 500 LOC pour garder des MR relisible.

Probleme : le premier agent n'arrive pas a tout ingérer sa fenetre de tokens est trop réduite. 
2eme version cli :
on essaye de decouper les input en bloc de scrs qui sont cohérents : les scrs qui ont des candidats FAISS qui pointe dans les memes dossiers sont regroupés.
on rajoute graphify pour naviguer plus vite et moins cher dans les repos mais a voir si ça marche vraiment.

benchmark graphify: petit projet -> ne reduit pas l'utilisation des tokens.
