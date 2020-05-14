# SQL missions
A SQL mission is a code mission with a remote database as service, [more information about service](../multi-service).
The main container will connect to the service, execute the user queries on it, then will check everything
went well.

There is two main kinds of SQL missions:

#### Read-only missions
For example your answer is something like
```SELECT * FROM public."myTable" ...```
In this case, you need to 
* Run the expected answer and store answer _**first !**_
* Run the given answer and store answer _**only after !**_
* Compare both answer

_You need to run your order first to avoid rollback the database in case of the user modifies it_


#### Read-write missions
This kind of mission is a little bit more complicated to validate. They mainly start with 
```DELETE/UPDATE/ALTER TABLE ... ```
In this case, you need to write a checker.sql (usually with a ```SELECT``` request) file in addition to success/query.sql. 
The success/query.sql will modifies the database (like the expected answer) and the checker.sql will select all interesting rows in the database

* Run the expected answer
* Run the checker.sql script and store the answer
* Rollback the database
* Run the given answer
* Run the checker.sql script and store the answer
* Compare both answer



### Tree example of SQL challenge
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
### Example
https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_sql