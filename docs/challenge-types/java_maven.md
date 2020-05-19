# Java Maven
When creating a Java Maven mission, you need to download all the project's dependencies in a build.sh with Maven.
```Bash
#!/bin/sh
# Script runned before building Docker image

# Download all dependencies of the project to put them into the Docker image via Dockerfile
# Here we have defined our dependencies into a jar directory
mvn -B dependency:copy-dependencies -DoutputDirectory=jar
```

Then the dependencies need to be put in a Dockerfile 
```Dockerfile
# Add all dependency jars
ADD jar src/main/java/jar
```

### Challenge.yml file
you have to complete the `challenge.yaml` file:
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

### Template and Success directories
The 'template/' directory contains the code that will be written by the user trying to solve the challenge.

The `success/` directory contains your solution given to the user when it succeeded the challenge.  
You can provide the implementation you wish.  

To test your program you can use [our CLI](https://pypi.org/project/deadlock-cli/):  
```Bash
> dcli run . # Will run template/
> dcli solve . # Will execute tests on template/
```

### Tree example of Java Maven challenge
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

### Example
[code_java_maven](https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_java_maven)