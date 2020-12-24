# Deadlock missions

---

## Overview

This documentation is mainly used to help everyone with the creation of their own learning content, through Deadlock platform.

## What is a mission ?
A mission is mainly composed of these elements:

* A "docs" folder: contains the files with the documentation to give the instructions to the candidate who will try to solve the mission. It can contains files with some hints too, to help the user.
* A "template" folder: code provided to the user
* A "success" folder: the challenge solution
* An "app" folder: logic to verify user code (some tests)
* A "challenge.yml" file: The mission descriptor

You can discover many elements on the user interface:

![Challenge interface](img/challenge-interface.png)

1. Documentation with briefing (main informations), hints
2. Provided code
3. Run button is used to execute code without any test
4. Submit button is used to execute test on user code

## Getting Started
Each mission came with a special structure. 
All the main files will be automatically generated if you use our [DCLI tool](https://github.com/deadlock-resources/dcli).
So it's pretty easy to start creating any challenge of your choice! 

### Install DCLI
Requirements:

* Docker ([as non-root user](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user))
* Python >= 3.2
* pip installed ([with python](https://pip.pypa.io/en/stable/installing/) or from your package manager)

Install [dcli](https://pypi.org/project/deadlock-cli/) package using pip:  
`pip3 install deadlock-cli`

Once dcli is installed on your computer, you can use the `dcli` command.  
Run `dcli --help` or `dcli version` to check that everything worked well.  

```bash
> dcli --help
# man page should be printed
> dcli version
current is 1.2.0
```

*If you have something like `command not found` or `module not found` when you run `dcli` try to export `/home/user/.local/bin/` to your $PATH.*


### Create your first coding mission

Let's create a Java mission as an example to explain you the concept behind the structure.
It's only an example to explain you how to create a coding mission. Once you have it, you will be able to create missions in every languages you want!

`dcli` is able to generate coding missions in other languages. 
You can see [different examples](https://github.com/deadlock-resources/challenge-examples).

Let's start!

Running the following command, you will init a Java coding mission:
```bash
> dcli gen java
```

In the following example, we will generate a simple mission where the user has to code a function which returns `Hello World!`.

![DCLI gen java](img/dcli-gen-java.gif)

You can explore the generated `code_hello_world` directory:
```bash
code_hello_world/
├── docs
│   ├── briefing.md
│   └── fr
│       └── briefing.md
├── src
│   └── main
│       └── java
│           ├── app
│           │   ├── Logger.java
│           │   ├── Solve.java
│           │   └── Run.java
│           ├── success
│           │   └── HelloWorld.java
│           └── template
│               └── HelloWorld.java
├── challenge.yml
├── Dockerfile
├── run.sh
└── thumbnail.png

```

In this challenge, the goal is simple: the candidate has to implement the `sayHello()` method, in the HelloWorld.java file in the `template` folder.  
All files under the `template` folder will be served to the user. You can create as many files as you want in this diretory.  

The `HelloWorld.java` file under the `success` folder will be served only when the user succeed the challenge. It contains your solution to the mission.
So the user will be able to see it once he has succeeded the challenge with his/her one.

You have to complete all `//TODO` in the coding files.  
Let's start with the `src/main/java/success/HelloWorld.java` file, the solution file we talked about above.  
```java
public static String sayHello() {
    //TODO write your own solution
    return null;
}
```

The `sayHello()` method has to return the string `"Hello World!"`.  
So you can write the folowing code in the `success/HelloWorld.java` file : 
```java
public static String sayHello() {
    return "Hello World!";
}
```

Once you have written the solution, you have to write a test suite allowing you to automatically test the candidate's solution.
This is done in the `src/main/java/app/Solve.java` file.

Dcli generates some code lines for you but have to complete with your own tests.
``` java
public static void main(String[] args) {
    try {
        // user result
        String userResult = HelloWorld.sayHello();
        // your solution result
        String expectedResult = success.HelloWorld.sayHello();
        //TODO you have to do different tests to be sure user has the good solution.
        // comparing userResult and expectedResult

        if (expectedResult.equals(userResult)) {
            // if all test passed successfully
            Logger.logSuccess();
        } else {
            Logger.logFail(expectedResult, userResult);
            System.exit(1);
        }
    } catch (RuntimeException e) {
        Logger.logException(e);
        // if something bad happened exit with error code
        System.exit(1);
    }
}
```
What it does is that if the function HelloWorld.sayHello() does not return "Hello World!" or throws an exception,
it logs an error and exits with an error code.

In general, there are 2 kinds of outputs you have to take into account.

1. Error: The code sent does not compile, does not have the right signature, code did not return the expected result, something bad happened.
2. Success: The code did complete normally and returned the expected result

A simple `Logger` class is also generated. You can now test your mission with the following command lines:
```Bash
> cd ./code_hello_world
> dcli run . # Run the program, execute the file `src/main/java/app/Run.java`
> dcli solve . # Run the program with your tests, execute the file `src/main/java/app/Solve.java`
```
You can try to modify the `HelloWorld.java` file under template package to reach the solution like you were the candidate.

### Documentation
The documentation is stored in **code_hello_world/docs/**.
It contains the Briefing to expose the problem your candidate has to solve and motivate him.
It should be written in Markdown, it supports HTML tags and LateX language.

* briefing.md: contains the default instructions
* debriefing.md: contains a text provided when user solve the challenge
* hint1.md: first hint user can unlock (optional)
* hint2.md: an other hint (optional)

examples of hints:  
**hint1.md**
```Markdown
The String that you need to return is the two words that you usually
display when you start learning a language for instance.
It can be considered as a greeting. (PS: the word is not "It Works")
```

**hint2.md**
```Markdown
Alright, the String is case sensitive, so you might want to try multiple cases.
Also, we were very emotional when we wrote this challenge, and decided to end the phrase with a "!"
```

**N.B.:** hint2 will always be given after hint1.

At this point, we have a functional Java application that will test the content of a **compiled** HelloWorld.class class and exit the relevant code.
If you want to understand more how the mission works and custom more your mission you can [read this](how-does-it-work.md).


## i18n
The default files into the docs folder contains the english translations.
If you want handle other languages you have to create new directories following this way:

* docs
    * briefing.md
    * fr
        * briefing.md

and so on.

## Level
Each mission has his own level

 - Jajarbinks (easiest)
 - Ewok
 - Padawan
 - Jedi
 - Master (hardest)  

When you create your own mission your can help you with the [references](./reference.md) to set a correct level
to your challenge.

## What's next
You can explore different types of challenge:

* [VsCode](challenge-types/vscode.md)
* [Multi language](challenge-types/metamorph.md)
* [Multi Service](challenge-types/multi-service.md)
* [Score](challenge-types/score.md)
* [SQL](challenge-types/sql.md)

