# VsCode challenge

Do you feel restricted with other challenge types ?  
Do you want to let your student enjoys a full editor ?

Let's do it with Deadlock in the browser!

![Demo Vscode gif](/challenge-documentation/img/demo-vscode.gif)


## How ?

You have to create the following files:

```S
├── base
│   ├── src   
│   │   ├── main   
│   │   │   ├── java                  
│   │   │   │   └── io
│   │   │   │       └── deadlock
│   │   │   │           └── demo
│   │   │   │               └── CdbApplication.java
│   │   │   └── resources/
│   │   └── test/
│   └── webapp/
├── challenge.yaml
├── Dockerfile
├── docs
│   └── briefing.md
└── thumbnail.png
```

* **base** directory containing user files, those files will be delivered to the user when the IDE starts.
* **docs** contains the briefing, user instructions, the briefing will be opened when the IDE starts. 
* **Dockerfile**
```Dockerfile
FROM registry.e-biz.fr/deadlock-public/deadlock-theia:latest

# You are free to install anything you want
# The package manager is *apt*

# destination paths are unchangeable
COPY base /project # copy user directory to /project
COPY docs /home/theia/docs # copy instructions
```
* **challenge.yaml** is the descriptor file
```Yaml
version: 0.1
name: code_persist_crud
label: Crud
description: This is your moment, you have to create your own CRUD. Your customer requested you to build a Computer DataBase application (codename *CDB*).
level: ewok # difficulty of the challenge [how it works](https://deadlock-resources.github.io/challenge-documentation/#level)
type: PERSISTENT # mandatory
xp: # xp tags, you are free to write your own
  programming: 1 # this is a weight, not a number
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
    crud: 9090
```
* thumbnail.png image challenge 

### Add image to the briefing
```
![toast](image:toast.jpg)
![Something Else](image:dir/else.png)
```
You must prefix your image path with *image:*


## How to test ?
```Bash
> cd ./code_persist_crud
> dcli run .
```
Then it will give you an address you can click on it or copy paste in your browser.

## Add services on startup

Let's say you need to start a service when the mission starts.
For instance a Postgres database.

You simply need to add a `startup.sh` script within your Docker image:  
`COPY startup.sh /deadlock/startup.sh`

and within your `startup.sh` for instance:  
```bash
#!/bin/sh

# Launch postgres service on startup
service postgresql start
```

The `startup.sh` script will be run when the Docker container starts.

*If you need to populate your database, it's better to do it within the Dockerfile (it will be faster than using the startup script):*  
```Dockerfile
# Postgresql installation
RUN apt-get -y update
RUN apt-get -y install postgresql

USER postgres

COPY db/sql /sql
# populate database
RUN /etc/init.d/postgresql start &&\
    psql --command "CREATE USER deadlock WITH SUPERUSER PASSWORD 'no-passwd';" &&\
    createdb -O deadlock deadlock-db &&\
    psql -d deadlock-db -U deadlock -f /sql/1__schema.sql -f /sql/2__entries.sql &&\
```
