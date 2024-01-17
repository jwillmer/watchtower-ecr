# WatchTower ECR
A docker image based on [v2tec/watchtower](https://github.com/v2tec/watchtower) for use with AWS ECR.

[![Docker Pulls](https://img.shields.io/docker/pulls/jwillmer/watchtower-ecr.svg?style=flat-square)](https://hub.docker.com/r/jwillmer/watchtower-ecr/)
[![Docker Stars](https://img.shields.io/docker/stars/jwillmer/watchtower-ecr.svg?style=flat-square)](https://hub.docker.com/r/jwillmer/watchtower-ecr/)

## Usage
Run the container with the following command:

```bash
docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /path/to/.docker/config.json:/config.json \
  -e "AWS_ACCESS_KEY_ID=<ACCESS_KEY_ID>" \
  -e "AWS_SECRET_ACCESS_KEY=<SECRET_ACCESS_KEY>" \
  rabaco/watchtower-ecr:latest --interval 45 --cleanup
```

Or using `docker-compose`:
```
watchtower:
    image: jwillmer/watchtower-ecr:latest
    container_name: watchtower
    restart: always
    command: --interval 45 --cleanup
    volumes:
        - /var/run/docker.sock:/var/run/docker.sock
        - /root/.docker/config.json:/config.json
    environment:
        - AWS_ACCESS_KEY_ID=${AWS_DOCKER_REGISTRY_KEY}
        - AWS_SECRET_ACCESS_KEY=${AWS_DOCKER_REGISTRY_SECRET}
```