```sh
docker network create network
```
```sh
docker-compose up
```
```sh
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```
```sh
docker exec gitlab-runner gitlab-runner register \
    --non-interactive \
    --url http://gitlab \
    --registration-token <token> \
    --description "docker dind runner" \
    --tag-list docker \
    --executor docker \
    --docker-image alpine:latest \
    --docker-network-mode host
```