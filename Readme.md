# Gitlab
Run your own Gitlab instance and Gitlab-Runner using Docker!
* Create a docker network
```sh
docker network create network
```
* Let docker-compose do it's magic
```sh
docker-compose up
```
* Add gitlab.local.com to your hosts file
```sh
127.0.0.1 gitlab.local.com
```
```
* Wait until the Gitlab instance is up and running
* Your root username is ```root``` what a surprise!
* Get the root password
```sh
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```
* Go to http://gitlab.local.com/admin/runners and get yourself the registration token
* Register the runner
```sh
docker exec gitlab-runner gitlab-runner register \
    --non-interactive \
    --url http://gitlab \
    --registration-token <token> \
    --description "docker dind runner" \
    --tag-list docker \
    --executor docker \
    --docker-host tcp://docker-daemon:2375/ \
    --docker-image alpine:latest \
    --docker-network-mode host
```
* Example ```.gitlab-ci.yml```
* Don't forget to tag your jobs with `docker`
```yml
job:
    tags:
        - docker
    image: "alpine:latest"
    before_script:
        - apk add zip
    script:
        - echo "Working fine!"
```
* Or edit your runner to pick up untagged jobs
* http://gitlab.local.com/admin/runners/:runner-id/edit
* Check the ```Run untagged jobs``` checkbox

## I wish you some successful pipelines!
