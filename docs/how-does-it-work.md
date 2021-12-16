# Comment ça marche ?
Si vous êtes ici, nous supposons que vous avez déjà parcouru [les bases](/#pour-commencer) et vous désirez en apprendre plus sur comment une mission fonctionne.  
Nous allons vous expliquer l'utilité de tous les fichiers d'une mission.

Pour être à l'aise avec la suite, vous devez posséder les bases en : 

* [Docker](https://www.docker.com/)
* Fichier Yaml

#### Dockerfile
Quand un candidat soumet son code, un conteneur Docker est créé.  
Le nom de l'image Docker sera le nom de votre mission préfixée de **code_**.  
**Important** : Vous devez définir CMD et ENTRYPOINT spécifiquement pour votre conteneur.  
Avant l'exécution de votre conteneur, le code du candidat est collé dans le dossier **template**.  
**L'emplacement** et **le contenu** de ce fichier vous est propre et doit être soumis dans le [descripteur](#descripteur-de-mission).

Une fois le code déployé dans le conteneur, ce dernier va s'exécuter jusqu'à la fin de vos instructions.
Rappelez-vous que les signaux STDOUT et STDERR seront affichés dans la console du candidat.
Une fois terminé, le code de sortie est vérifié.

Si le **code de sortie** est **0**, la mission est un **succès**.  
**Sinon**, cela veut dire que le candidat a **échoué**.

Vous pouvez personnaliser le Dockerfile à volonté en incluant par exemple des librairies externes pour permettre au candidat
d'avoir accès à encore plus de fonctionnalités !

Exemple d'une mission python incluant les librairies **nymphy, sklearn et pandas**
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
L'étape de build est effectuée une foi seulement lorsque la mission est acceptée par l'équipe Deadlock.

#### Descripteur de mission
Chaque mission a son propre descripteur disponible dans challengename/challenge.yml.  
Il est utilisé pour créer le conteneur de mission et récupérer les spécificités de la mission concernant les langages et fichiers cibles

```bash
version: 1.0 # A incrémenter si le code évolue
name: code_halloween_candy # Le nom de la missions. Il DOIT être identique au nom du dossier de la mission
label: Halloween Candy # Le libellé de la mission
description: Help your brother split his halloween candy # La description de la mission en anglais
level: jarjarbinks # Le niveau de la mission. Du plus facile au plus difficile : jarjarbinks, ewok, padawan, jedi, master
type: CODING # Le type de la mission. Ici : coding game
meta:
  private: true # Si true, la mission sera uniquement visible sur votre instance "ecole.deadlock.io), par défaut : false --> visible par tout le monde.
xp: # le nombre de points d'expérience que cette mission rapporte dans chaque domaine listé en dessous
  programming: 1 # Il s'agit d'un poids et non d'un simple nombre.
  java: 1
coding: # Spécifique au challenge de type code
  templateDirectory: src/java/main/template # Le code fournit au candidat
  successDirectory: src/java/main/success # La solution de la mission
  target: CandySplitter.java # Le path du fichier cible considéré comme fichier Main
  editorMode: java # Le langage à afficher dans l'éditeur Web
```
