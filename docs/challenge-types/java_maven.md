# Java Maven
Lorsque vous créez une mission Java Maven, vous devez télécharger toutes les dépendances du projet dans un fichier `build.sh` en utilisant Maven.
```Bash
#!/bin/sh
# Script exécuté avant le build de l'image Docker

# Télécharge toutes le dépendances du projet pour les ajouter à l'image Docker via le Dockerfile
# Ici, nous avons défini nos dépendances dans un jar
mvn -B dependency:copy-dependencies -DoutputDirectory=jar
```

Ensuite, les dépendances sont ajouté au Dockerfile 
```Dockerfile
# Ajoute les jars de toutes les dépendances
ADD jar src/main/java/jar
```

### Fichier Challenge.yml
Vou devez compléter le fichier `challenge.yaml` : 
```Yaml
version: 1.0
name: code_calculator
label: Calculator challenge
description: Implement calculator operations
level: ewok
type: CODING
xp:
  java: 1
  programming: 1
coding:
  templateDirectory: src/main/java/template
  successDirectory: src/main/java/success
  target: Calculator.java
  editorMode: java
```

### Dossier Template et Success
Le dossier `template/` contient le code écrit par le candidat tentant de résoudre la mission.

Le dossier `success/` contient votre solution qui sera donnée au candidat lorsqu'il aura réussi la mission.  
Vous pouvez fournir l'implémentation de solution que vous désirez.  

Pour tester votre programme, vous pouvez utiliser notre [CLI](https://pypi.org/project/deadlock-cli/):  
```Bash
> dcli run . # Exécture template/
> dcli solve . # Exécute les tests de template/
```

### Exemple d'arborescence d'une mission Java Maven
```
├── challenge.yaml
├── docs
│   ├── ...
├── jar
├── build.sh
├── Dockerfile
├── run.sh
├── pom.xml
├── src
│   ├── main
│       └── java
│           ├── app
│           │   ├── Logger.java
│           │   ├── Run.java
│           │   ├── Solve.java
│           └── success
│               └── Calculator.java
│               └── CalculatorTest.java
│           └── template
│               └── Calculator.java
│               └── CalculatorTest.java
```

### Exemple
[code_java_maven](https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_java_maven)
