# docker-cheat-sheet

##### Best way to clean up Docker data safely:
```bash
docker system prune -a --volumes
```


#### Networks:
---
##### Remove all Networks:
```bash
docker network prune -f
```
or
```bash
docker network rm $(docker network ls | grep "bridge" | awk '/ / { print $1 }')
```

#### Volumes:
---
##### Remove all dangling volumes:
```bash
docker volume rm $(docker volume ls -qf dangling=true)
```

#### Images:
---
##### Remove only dangling images:
```bash
docker rmi $(docker images -f dangling=true -q)
```
###### Remove all images:
```bash
docker rmi $(docker images -f -a -q)
```
###### Remove images with pattern:
```bash
docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi
```
###### List dockerfile commands
```bash
docker history --no-trunc <image>
```

#### Containers:
---
##### Remove all stopped containers:
```bash
docker rm $(docker ps -a -q)
```
or
```bash
docker container prune
```
##### Docker Run and remove  (my-container) container when stopped:
```bash
docker run --rm -it my-docker 
```
##### Remove all containers forcefully:
```bash
docker rm --force $(docker ps -a -q)
```
or
```bash
docker container prune -f
```
#### Exec inside a container
```bash
docker exec -it <container_name|contianer_id> bash
```

#### Registry:
---
##### Acessing Registry (v2) with curl:
Note: for protected registry, basic auth argument `username:password`.
##### List repositories:
Docker registry is running in a local container.
```bash
curl -X GET http://localhost:5000/v2/_catalog
```
##### List tags from a repository:
```bash
curl -X GET http://localhost:5000/v2/<repository>/tags/list
```

## Additional guides

[Remote Docker setup (over TCP port)][1]  
[Install Docker using snap][2]  
[Installing dokcer-compose (linux)][3]  


## Other Cheat Sheets

[Git][101]  
[SSH][102]  
[Docker Compose][103]

## References
- [Official Docker Documentation][201]


[1]: https://gist.github.com/WSMathias/ee53251a5f778756f8ab43fb2c83c33f
[2]: https://gist.github.com/WSMathias/a3e48b75720a71dd3b7f77717bcae7c1
[3]: https://gist.github.com/WSMathias/3a0b5e0b68a2f6b32c47b116c8e2e7f6

[101]: https://github.com/WSMathias/Git-Cheat-Sheet/blob/master/README.md
[102]: https://gist.github.com/WSMathias/ee53251a5f778756f8ab43fb2c83c33f
[103]: https://gist.github.com/WSMathias/24cf2eed19195497699a2956cb27e1e9

[201]: https://docs.docker.com/reference/cli/docker/
