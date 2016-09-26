# Networking

Docker provides built-in networking between containers on a single node, containers on multiple nodes, and node-to-node networking. Docker provides three networks out of the box. These networks can be listed with the following command:

```bash
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
434fb7e34464        bridge              bridge              local               
806de3f78bd4        host                host                local               
e75575b66a46        none                null                local   
```

By default, all containers are added to the `bridge` network unless it is run with the `--network=[name]` flag. The bridge network is also referred to as the `docker0` network part of all Docker installations. The other two default networks, `host` and `none` are required by Docker to run successfully. 
