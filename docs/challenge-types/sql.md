# Missions SQL
Une mission SQL est une mission classique de code avec une base de donnée distante injectée via un service. Plus d'infos sur les [services](../multi-service)   
Le conteneur principal se connecte au service, exécute les requêtes du candidat puis vérifie que tout s'est bien déroulé.

Il y a deux types principaux de missions SQL :

#### Missions en lecture seule
Par exemple, la réponse à votre mission pourrait ressembler à  
```SELECT * FROM public."myTable" ...```  

Dans ce cas vous avez besoin de : 

* Exécuter la réponse attendue et stocker le résultat dans _**first !**_
* Exécuter la réponse du candidat et stocker le résultat dans _**only after !**_
* Comparer les deux réponses

_Il est nécessaire d'exécuter votre réponse en premier afin d'éviter tout retour en arrière de la base de donnée que le code du candidat pourrait provoquer._


#### Missions d'édition
Ce type de mission est un peu plus compliqué à valider. Elles débutent généralement par :  
```DELETE/UPDATE/ALTER TABLE ... ```

Dans ce cas, Il est nécessaire d'écrire un fichier `checker.sql` (généralement avec une requête ```SELECT```) en plus du fichier `success/query.sql`.  
Le fichier `success/query.sql` modifie la base de données (c'est la réponse attendue) et le fichier `checker.sql` sélectionne toutes les lignes qui nous intéressent dans la base de données

* Exécuter la réponse attendue
* Exécuter le script `checker.sql` et stocker le résultat
* Faire un retour-arrière sur la base de données
* Exécuter la réponse donnée par le candidat
* Exécuter le script `checker.sql` et stocker le résultat
* Comparer les deux réponses



### Exemple d'arborescence d'une mission SQL
```
├── app
│   ├── pom.xml
│   └── src
│       └── main
│           ├── java
│           │   ├── Core.java
│           │   ├── DBComparator.java
│           │   ├── QueryResult.java
│           │   └── ScriptRunner.java
│           └── resources
│               └── db.properties
├── challenge.yaml
├── checker.sql
├── Dockerfile
├── docs
│   ├── ...
├── run.sh
├── services
│   └── db
│       ├── Dockerfile
│       ├── entries
│       │   ├── 1-schema.sql
│       │   ├── 2_1-data-person.sql
│       │   ├── 2_2-data-crime.sql
│       │   └── 2_3-data-crime_person.sql
│       ├── init-and-dump.Dockerfile
│       ├── initiator
│       │   ├── pom.xml
│       │   └── src
│       │       └── main
│       │           └── java
│       │               ├── Core.java
│       │               ├── Crime.java
│       │               ├── CriminalRecord.java
│       │               └── User.java
│       ├── README.md
│       ├── run-dump.sh
│       ├── service.yaml
│       └── wait-for-it.sh
├── success
│   └── query.sql
├── template
│   └── query.sql
└── thumbnail.png
```
### Exemple
[https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_sql](https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_sql)
