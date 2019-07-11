# Démarrer avec Apache Beam

> Work in progress, stay tuned.

Une explication simple de qu'est-ce que c'est que le traitement par lots (batch) et le traitement par flux (stream) avec Apache Beam et Cloud Dataflow.

## Le traitement par lots (batch), qu’es aquò ?

Imagine un mec qui s'appelle Bob. Bob c'est un développeur talentueux qui a conçu un jeu multi-joueurs en ligne sur smartphone. Bob veut analyser et comprendre le comportement de ses joueurs afin d'ajouter du contenu ayant du sens et susceptible de plaire. Pour cela, il enregistre toutes les actions des joueurs dans un fichier de logs horodaté, qui correspond à un jour de la semaine, pour le traiter plus tard :

* *X a tué Y - timestamp*
* *X a acheté une super épée qui tue à 0.80€ dans la boutique - timestamp*
* *X a battu le Dragon Rouge - timestamp*
* *X a crash sur Samsung S9 après avoir changé de zone - timestamp*

Ok. Nous sommes Mardi et Bob décide de lancer son processus de traitement de données sur le fichier de logs de la veille. Par le biais de différentes opérations de transformation (map, reduce, filter, group by key, combine...), il va pouvoir agréger des données et extraire des informations pertinentes comme le nombre de crashs, le nombre de fois qu'un Boss a été battu, les top 5 produits qui se vendent le plus dans sa boutique etc. Ensuite, Bob n'a plus qu'à analyser les données en output et prendre des décisions.

On parle donc ici de traitement par lots.

## et le traitement par flux... (stream) ?

Bob est pas très content. En effet, des joueurs malintentionnés abusent des quelques failles de son jeu pour générer de l'argent et des items. Et ça l’agace car il ne peut sanctionner les joueurs qu'après avoir analysé le fichier de logs de la veille ! 

Alors, pour ne plus attendre, Bob décide d'intégrer un pipeline d'agréation de données en temps-réel à son processus. Via un pattern diffuseurs-abonnés (Publisher/Subscriber), Bob diffuse certains événements qui vont être consommés et traités aussitôt par son pipeline. En quasi-temps-réel, il voit apparaitre sur son tableau de bord des résultats spéculatifs sur les transactions qu'effectuent les joueurs. Bob est ravi car il est maintenant capable de détecter rapidement les anomalies et les fraudes qui surviennent dans son jeu afin de sanctionner les malotrus.

On parle ici d'un traitement par flux, caractérisé par une latence faible et des résultats spéculatifs en temps-réel.

> Todo:

## Architecture Lambda

- Ok 2 pipelines pour stream et batch c'est bien, mais chiant à maitenir un système aussi complexe.
- Avantages/Inconvéniants/Solutions

## Apache Beam

- Modèle de programmation unifié
- Tente de résoudre les problèmes de l'archi Lambda
- PCollections, PTransforms, ParDo, DoFn, I/Os
- Fenêtrage, déclencheurs, filigrane
- Sérialisation

## Cloud Dataflow

- Service managé, no ops, no bouttons, no mains, no cerveau de Google
- Execute des jobs de batch et stream
- Parallélisme
- Cluster de X VM Compute Engine (worker nodes)

## Cloud Pub/Sub

## Exemple d'un jeu multijoueurs


