# Multi-service missions
Sometimes, you may have to declare multiple services in your challenge.
This feature is fully supported and uses containers within one network.

Here is a walkthrough of adding another service named **db**.
In the main folder of your challenge, create the directories **code_your_mission/services/db**.  
This directory will contain your service files.

In this folder, you must declare at least two files:  

- The service descriptor **service.yaml**
- The service container **Dockerfile**


### The service descriptor
The service descriptor can expose ports and a specific alias (which must be the service name).
Following on our example, the **db** service would be:
```yaml
name: db
exposed_ports:
  - 5432
```

You can find an example of a multi services mission though [SQL type challenge](./sql).