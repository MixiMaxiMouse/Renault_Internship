# Renault_Internship
End of studies internship at Reanult - Ampere Software technologies (AST)

Maxence Maury

## Semaine 1 [23 mars - 27 mars]

Maxime Dandre, PO et tuteur de stage

Arrivée Lundi 23 mars.
Installation du poste, pc windows et pc fixe linux accessible en remote.
Beaucoup de demandes de droits.
Re definition plus precise du sujet de stage: Outil de tracking des exigeances pour la traçabilité. 
commencement du sujet de stage:
Premier MVP defini avec Maxime.
MVP : un tableau de bord web pour voir le pourcentage d'exigeances (et autres indicateurs) testés dans le code. Code en python.
Les exigeances sont definies dans l'application CodeBeamer. Les tests des exigeances sont dans deux projets gitlab en Rust et Kotlin DISCO et DriverUI (Software pour les ecrans du tableau de bord des voitures Renault).
Avancement sur le MVP : iterations de poc et validation par Maxime
- Mercredi 25 mars premier poc fait en 3 jours, validé par Maxime: juste un dashboard sur des donnés mockées. Camembert de % d'exigeances testés, liste des non testés.
- Lundi 30 mars deuxieme poc validé par Maxime: Dashboard plus complet basé sur un extract codebeamer en excel et sur les vrai repos git des projets. Rajout gestion depot git et gestion fichier excel.

Suite du stage : Utiliser des LLMs pour automatisation de la verification des tests et de l'eventuel implementation de ceux ci.

## Semaine 2 
Formation opencode, et copilot. Renault cherche a utiliser l'IA de plus en plus et cherche des gens formé a l'IA.
fin de l'implem du dashboard MVP, dockerisation et exposition sur reseau interne a l'adresse du pc linux (qui tourne en permanance avec l'appli)
Mise en place petite CI locale pour valider qualité de code, sous forme de script. gitlab CI trop compliqué car pas de runner et projet privé (pas d'autres contributeurs) donc pas besoin.
Cleanup de l'appli et premier livrable au PO. Validé.
Mise en palce d'un vrai environnement de dev sur une autre branche avec un autre port d'exposition. jusqu'ici le dev servait de prod comme il n'y avait toujours pas de version stable.
cyber training et codebeamer training

