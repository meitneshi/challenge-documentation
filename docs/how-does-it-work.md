# How does it work ?
If you are here, you already read the [Getting Started](/#getting-started) and you want to explore more about how a challenge works.
We are going to explain you different files, 


To be sure to understand the next parts you have to be familiar with:

* [Docker](https://www.docker.com/)
* Yaml

#### Dockerfile
When your candidate submits his code, a Docker container will be created.
The name of the Docker image will be your challenge name, prefixed with **code_**.  
**Important:** your container should have its own CMD or ENTRYPOINT defined.
Before your container is executed, your candidate code will be pasted within **template** folder.
**Where** and **what** this file is is entirely up to you and shall be submitted in the [descriptor](#challenge-descriptor).

Once the code is inside the container, your container will be ran until completion.
Note that the STDOUT and STDERR signals will be streamed to the candidate.
Once it completes, the exit code will be checked.

If the **exit code** is **0**, the challenge was **completed** successfully.
**Otherwise**, it means the candidate has **failed**.

You can custom the Dockerfile has you wish, include external library to allow your user to have new experiences !  
Example of a python challenge with **nymphy, sklearn and pandas libraries**:  
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
The build step is done only one time when your challenge is accepeted by the Deadlock team.


#### Challenge descriptor
Each challenge has its own challenge descriptor in challengename/challenge.yaml.
It is used to create the challenge container and retrieve your specifications regarding the language and file target.

```
name: code_halloween_candy # your challenge name. MUST be equal to the challenge folder
label: Halloween Candy # your challenge label
description: Help your brother split his halloween candy # your challenge description, in english
level: jarjarbinks # your challenge level. From easiest to hardest: jarjarbinks, ewok, padawan, jedi, master
type: CODING # this is a coding game
xp: # the experience it should bring. any label is supported
  programming: 1 # this is a weight, not a number
  java: 1
coding: # coding game specifics
  templateDirectory: src/java/main/template # code provided to the user
  successDirectory: src/java/main/success # solution of the challenge
  target: CandySplitter.java # the target file path, consider as Main file
  editorMode: java # the language to be displayed by the web editor
```