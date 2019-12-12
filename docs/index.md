# Deadlock missions

---

## Overview

This documentation is mainly used to help everyone with the creation of their own learning content, through Deadlock platform.

## What is a mission ?
A mission is mainly these elements:

* A documentation: instructions for the user
* A template folder: code provided to the user
* A success folder: solution of the challenge
* An app folder: logic to verify user code
* The mission descriptor: challenge.yml
* Many hints: You can add different hints, each one could be unlock with token, user unlock 

You can discover many elements on the user interface:

![Challenge interface](img/challenge-interface.png)

1. Documentation with briefing (main informations), hints
2. Provided code
3. Run button is used to execute code without any test
4. Submit button is used to execute test on user code

## Getting Started
Each mission came with a special structure, it will be provided by our [DCLI tool](https://github.com/deadlock-resources/dcli)
So it's pretty easy to start any challenge, you will just have to care what you want to deliver to your users.

### Install DCLI
Requirements:

* Python >= 3.2
* pip installed ([with python](https://pip.pypa.io/en/stable/installing/) or from your package manager)

Install `dcli` package using pip:  
**Not available on pypi, [install from sources](https://github.com/deadlock-resources/dcli#install-from-sources).**

Then you shoud have `dcli` command on your system. Run `dcli --help` to check that everything worked well.
``` bash
$ dcli --help
man page should be printed
```

### Create your first code challenge
Let's create a Java mission to explain you the concept behind the structure.
```bash
dcli gen java
```
We will generate a simple mission where the user must return `Hello World!`.

![DCLI gen java](img/dcli-gen-java.gif)

You can explore the generated `code_hello_world` directory:
```
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

As you saw it, the goal is simple, implement the `sayHello()` method within `template` package.
All files under `template` package will be served to the user, you can create as much as you want.
The `HelloWorld.java` file under `success` package will be served only when the user succeed the challenge.

You have to complete all `//TODO` present in the code.  
Let's start with `src/main/java/success/HelloWorld.java`, this is the solution file.  
```java
public static String sayHello() {
        //TODO write your own solution
        return null;
}
```
Pretty simple the method has to return `"Hello World!"`.  
Next part is to compare the user result with the expected result, this part is done under `src/main/java/app/Solve.java`.
Dcli generates some part of code for you but have to complete with your own logic.
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
```bash
cd ./code_hello_world
dcli run . # Run the program, execute the file `src/main/java/app/Run.java`
dcli solve . # Run the program with your tests, execute the file `src/main/java/app/Solve.java`
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
The String that you need to return is the two words that you usually display when you start learning a language for instance.
It can be considered as a greeting. (PS: the word is not "It Works")
```

**hint2.md**
```Markdown
Alright, the String is case sensitive, so you might want to try multiple cases. Also, we were very emotional when we wrote this challenge, and decided to end the phrase with a "!"
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

* [Hack](challenge-types/hack.md)
* [Multi Service](challenge-types/multi-service.md)
* [SQL](challenge-types/sql.md)


## Getting help
To get help with Deadlock Challenge, please use the [GitHub mission example issues](https://github.com/deadlock-resources/challenge-examples/issues) or [GitHub mission documentation issues](https://github.com/deadlock-resources/challenge-documentation/issues).