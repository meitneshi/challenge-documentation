# How does it work ?

If you are here, you may have already read the [Getting Started](/#getting-started) docs.
If not, I advice you to read it before going further through this documentation.

So you are still here, which means you want to know more about how a mission works.

To be sure you understand easily the next sections, you have to be familiar with these two following concepts:
* [Docker](https://www.docker.com/)
* Yaml file

#### Dockerfile

When your candidate submits his/her code, a Docker container will be created.
The Docker image name will be your mission name, prefixed with **code_**.  
*example* : A container from the image "code_caesar_decipher" will be created for a mission called "caesae_decipher".  

**Important:** Your container should have its own CMD or ENTRYPOINT defined.  

Before your container is executed, your candidate code will be pasted within **template** folder.  
Once the code is inside the container, your container will be run until completion.
Note that the STDOUT and STDERR signals will be streamed to the candidate.  

When the code exeuction finished, the exit code will be checked to know if the candidate code is right or wrong:
If the **exit code** is **0**, the mission was **completed** successfully.
**Otherwise**, it means the candidate has **failed**.

You can custom the Dockerfile to include external libraries to allow your user to have new experiences!  

Example of a python mission with **nymphy, sklearn and pandas** libraries:  
```Dockerfile
FROM python:3.7-slim
RUN pip install numpy sklearn pandas
WORKDIR /
COPY src src
COPY wine.csv src/main/
COPY run.sh /
RUN chmod +x run.sh
ENTRYPOINT ["/run.sh"]
```

The build step is done only once, when your mission is accepeted by the Deadlock team.


#### Mission descriptor
Each mission has its own mission descriptor in **challenge-name/challenge.yaml**.
It is used to create the mission container and retrieve your specifications regarding the language and file target.

```bash
version: 1.0 # You have to increase the version if you have changed something in your code
name: code_halloween_candy # your mission name. MUST be equal to the mission folder
label: Halloween Candy # your mission label
description: Help your brother split his halloween candy # your mission description, in english
level: jarjarbinks # your mission level. From easiest to hardest: jarjarbinks, ewok, padawan, jedi, master
type: CODING # this is a coding game
meta:
  private: true # if true mission will only be visible on your instance (youSchool.deadlock.io), default to false, visible by everyone.
xp: # the experience it should bring. any label is supported
  programming: 1 # this is a weight, not a number
  java: 1
coding: # coding game specifics
  templateDirectory: src/java/main/template # code provided to the user
  successDirectory: src/java/main/success # solution of the challenge
  target: CandySplitter.java # the target file path, consider as Main file
  editorMode: java # the language to be displayed by the web editor
```
