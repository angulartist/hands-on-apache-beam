# Démarrer avec Apache Beam

> Work in progress, stay tuned.

Une explication simple de qu'est-ce que c'est que le traitement par lots (batch) et le traitement par flux (stream) avec Apache Beam et Cloud Dataflow.

<p align="center">
  <img width="625" height="352" src="https://www.geek.com/wp-content/uploads/2017/10/razer-phone-top-625x352.jpg">
</p>

## Le traitement par lots (batch), qu’es aquò ?

Imagine un mec qui s'appelle Bob. Bob c'est un développeur talentueux qui a conçu un jeu multi-joueurs en ligne sur smartphone. Bob veut analyser et comprendre le comportement de ses joueurs afin d'ajouter du contenu ayant du sens et susceptible de plaire. Pour cela, il enregistre toutes les actions des joueurs dans un fichier de logs horodaté, qui correspond à un jour de la semaine, pour le traiter plus tard :

* *X a tué Y - timestamp*
* *X a acheté une super épée qui tue à 0.80€ dans la boutique - timestamp*
* *X a battu le Dragon Rouge - timestamp*

...

Nous sommes Mardi et Bob décide de lancer son processus de traitement de données sur le fichier de logs de la veille. Par le biais de différentes opérations de transformation (map, reduce, filter, group by key, combine...), il va pouvoir agréger des données et extraire des informations pertinentes comme le nombre de fois qu'un Boss a été battu, les top 5 produits qui se vendent le plus dans sa boutique, L'EXP moyen gagné par joueur etc. Ensuite, Bob n'a plus qu'à analyser les données en output et prendre des décisions.

> On parle donc ici de traitement par lots, caractérisé par un large volume de données traité avec une latence haute (heures, jours, semaines...). Les événements sont loggés et sockés pour être traités plus tard. Souvent le découpage des fichiers se fait par heures, jours, semaines, mois. Le traitement par lots est utile dans le cas où l'on n'a pas besoin de temps-réel mais où la complétude et l'exactitude des données sont des points cruciaux.

## et le traitement par flux... (stream) ?

Bob est pas très content. En effet, des joueurs malintentionnés abusent des quelques failles de son jeu pour générer de l'argent et des items. Et ça l’agace car il ne peut sanctionner les joueurs qu'après avoir analysé le fichier de logs de la veille ! 

Alors, pour ne plus attendre, Bob décide d'intégrer un pipeline d'agrégation de données en temps-réel à son processus. Via un pattern diffuseurs-abonnés (Publisher/Subscriber), Bob diffuse certains événements qui vont être consommés et traités aussitôt par son pipeline. En quasi-temps-réel, il voit apparaitre sur son tableau de bord des résultats spéculatifs sur les transactions qu'effectuent les joueurs. Bob est ravi car il est maintenant capable de détecter rapidement les anomalies et les fraudes qui surviennent dans son jeu afin de bannir les malotrus.

> On parle ici d'un traitement par flux, caractérisé par une latence faible et des résultats spéculatifs en temps-réel. Les événements sont publiés, à la volée, continuellement, dans un service de messagerie (ex: Cloud PubSub / Apache Kafka) qui s'occupera de les distribuer aux différents abonnés (ex: un pipeline de traitement par flux). Le traitement par flux est utile dans les cas où l'on désire une latence faible (secondes, millisecondes) et des résultats spéculatifs en quasi temps-éel :
* Systèmes de recommendation (ex: playlists Spotify, produits Amazon, trending topics Twitter...)
* Détection de fraudes (ex: Finances, jeux multi-joueurs...)
* Détection d'anomalies (ex: Capteurs de température dans une zone critique, monitoring de Web-Services...)
* Analyse du trafic routier etc.


> Todo: Ecrire des trucs en bas.

## Architecture Lambda

- Ok 2 pipelines pour stream et batch c'est bien, mais chiant à maitenir un système aussi complexe.
- Avantages/Inconvéniants/Solutions

## Apache Beam

- Modèle de programmation unifié
- Tente de résoudre les problèmes de l'archi Lambda
- PCollections, PTransforms, ParDo, DoFn, I/Os
- Fenêtrage, déclencheurs, filigrane
- Déduplication
- Event-time vs Processing-time
- Sérialisation

## Cloud Dataflow

- Service managé, no ops, no bouttons, no mains, no cerveau de Google
- Execute des jobs de batch et stream
- Parallélisme
- Cluster de X VM Compute Engine (worker nodes)

## Cloud Pub/Sub

- No ops, global scale bus de messagerie
- Publisher/Subscriber pattern
- Glue

## Exemple d'un jeu multi-joueurs

