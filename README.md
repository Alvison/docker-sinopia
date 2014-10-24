## Sinopia (Docker Image)

Sinopia is a private npm repository server

### Installing Image

`docker pull keyvanfatehi/sinopia:0.13.0`

### Creating Container

`docker run --name sinopia -d -p 4873:4873 keyvanfatehi/sinopia:0.13.0`

### Setting Registry

`npm set registry http://<docker_host>:4873/`

### Determining Username and Password

`docker logs sinopia`

### Modify configuration

```
docker stop sinopia
docker run --volumes-from sinopia -it --rm ubuntu vi /opt/sinopia/config.yaml
docker start sinopia
```

### Backups

`docker run --volumes-from sinopia -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /opt/sinopia`

Alternatively, host path for /opt/sinopia can be determined by running:

`docker inspect sinopia`

### Restore

```
docker stop sinopia
docker rm sinopia
docker run --name sinopia -d -p 4873:4873 keyvanfatehi/sinopia:0.12.0
docker stop sinopia
docker run --volumes-from sinopia -v $(pwd):/backup ubuntu tar xvf /backup/backup.tar
docker start sinopia
```

## Links

* [Sinopia on Github](https://github.com/rlidwka/sinopia)
