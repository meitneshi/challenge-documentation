# Missions multi-service
Parfois, vous devrez déclarer plusieurs services dans votre mission.
Cette fonctionnalité est totalement supporter et utilise les réseaux de conteneurs (container network).

Nous allons vous guider dans le processus d'ajout d'un service supplémentaire appelé **db**.
Dans le dossier principal de votre mission, créer les dossiers **code_your_mission/services/db**.  
Ce dossier va contenir les fichiers de votre service.

Dans ce dossier, vous devez créer au moins ces deux fichiers :  

- Le descripteur du service **service.yaml**
- Le conteneur du service **Dockerfile**


### Le descripteur du service
Le descripteur du service expose les ports et un alias spécifique (qui doit être le nom du service).
En suivant cet exemple, le service ***db*** ressemblerait à :
```yaml
name: db
exposed_ports:
  - 5432
```

Un exemple de mission multi-services est disponible [ici](../sql).
