# Gestion des répertoires externes **[BETA]**

## Vue d'ensemble

Cette documentation est principalement destinée à aider les professerus, les créateurs de contenus ou les administrateurs
pour gérer des répertoires personnalisés sur la plateforme Deadlock.


## Qu'est-ce qu'un répertoire de missions Deadlock ?


Un répertoire de missions Deadlock est principalement composé de deux parties : 

- un dossier **resources** qui contient toutes vos missions 
- un **registre** qui contient les images docker de chacune de vos missions.


Une mission Deadlock classique devrait ressembler à cela :

```
├── README.md
├── build
│   ├── build-image.sh
│   └── parse_yaml.sh
└── resources
    └── code_palindrome_test
        ├── Dockerfile
        ├── challenge.yaml
        ├── docs
        │   ├── ...
        ├── run.sh
        ├── src
        │   └── ...
        └── thumbnail.png
```


Faîtes un fork de [ce template][template_repo] pour avoir un repository prêt à l'emploi. Il ne restera plus qu'à ajouter vos missions.
N'hésitez pas à vous en inspirer.

## Plus d'infos

* [Le guide du mainteneur](maintainer-guide.md) si vous êtes un créateur de missions et vous désirez les partager
* [Le guide de l'admin Deadlock](admin-guide.md) si vous êtes un administrateur d'instance Deadlock et que vous 
désirez ajouter un répertoire

[template_repo]: https://git.e-biz.fr/deadlock-public/deadlock-challenges-example
