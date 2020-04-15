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
Remove images with pattern:
```bash
docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi
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
