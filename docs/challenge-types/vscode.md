# VsCode challenge

Do you feel restricted with other challenge types ?  
Do you want to let your student enjoys a full editor ?

Let's do it with Deadlock in the browser!

![Demo Vscode gif](/challenge-documentation/img/demo-vscode.gif)


## How ?

You have to create the following files:

```S
├── base
│   └── src
│       └── main
│           └── java
│               └── io
│                   └── deadlock
│                       └── sort
│                           └── Main.java
├── challenge.yaml
├── Dockerfile
├── docs
│   └── briefing.md
└── thumbnail.png
```

* **base** directory containing user files 
* **docs** contains the briefing, user instructions 
* **Dockerfile**
```Dockerfile
FROM registry.e-biz.fr/deadlock-public/deadlock-theia:latest

COPY base /project # copy user directory to /project
COPY docs /home/theia/docs # copy documentation 
```
* **challenge.yaml** is the descriptor file
```Yaml
version: 0.1
name: code_persist_fibo
label: Fibonacci
description: Implement Fibonacci algorithm
level: ewok # difficulty of the challenge
type: PERSISTENT # mandatory
xp: # xp tags, you are free to write your own
  programming: 1
  java: 1
coding:
  userDirectory: base
resources: # Resources given for the container, don't touch it if you are not comfortable with
  cpuLimit: "1200m"
  memoryLimit: "1200Mi"
  cpuRequest: "1000m"
  memoryRequest: "1000Mi"
persistent:
  ports: # ports you want to let open for the user
    web: 3000 # mandatory
    test: 9090
```
* thumbnail.png image challenge 


## How to test ?
```Bash
> cd ./code_persist_fibo
> dcli run .
```
Then it will give you an address you can click on it or copy paste in your browser.