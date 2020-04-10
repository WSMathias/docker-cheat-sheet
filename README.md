# docker-cheat-sheet

Best way to clean docker safely:
```bash
$ docker system prune -a --volumes
```
Remove all container Forcefully:
```bash
docker rm --force $(docker ps -a -q)
# or
docker container prune -f
```
Remove all Networks:
```bash
docker network prune -f
# or
docker network rm $(docker network ls | grep "bridge" | awk '/ / { print $1 }')
```

Remove all dangling volumes:
```bash
docker volume rm $(docker volume ls -qf dangling=true)
```
Remove only dangling images:
```bash
docker rmi $(docker images -f dangling=true -q)
```

Remove all images:
```bash
docker rmi $(docker images -f -a -q)
```

Remove all stopped containers:
```bash
docker rm $(docker ps -a -q)
# or 
docker container prune
```

Docker Run and remove  (my-container) container when stopped:
```bash
docker run --rm -it my-docker 
```

### Remote Docker setup
Open docker service file
```bash
sudo vi /lib/systemd/system/docker.service
```
Append `-H tcp://0.0.0.0:2375` to ExecStart value
ex:
```bash
ExecStart=/usr/bin/docker daemon -H fd:// -H tcp://0.0.0.0:2375
```
Run following for applying changes
```bash
sudo systemctl daemon-reload
```
then 
```bash
sudo systemctl restart docker
# or
sudo service docker restart
```

To access remote docker
```bash
export DOCKER_HOST=tcp://0.0.0.0:2375
docker version
```
Unset DOCKER_HOST to use local docker again

On VScode setting add `"docker.host": "tcp://0.0.0.0:2375"`

