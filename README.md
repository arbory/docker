# Arbory Docker images

This repository contains Dockerfiles to create images with all necessary
dependencies for Arbory.

## Supported tags and respective Dockerfile links

- `8.0`, `8.0-mysql`, `latest`
- `7.4`, `7.4-mysql`, `latest`
- `7.4-postgres`
- `7.3`, `7.3-mysql`
- `7.3-postgres`
- `7.2`, `7.2-mysql`, `7.2-mysql-dev`
- `7.2-postgres`
- `7.1`, `7.1-mysql`
- `7.1-postgres`

## Quick reference

- Where to get help: [Stack Overflow][stack_overflow_docker_tag]
- Where to file issues: [GitHub issues][github_issues]

[stack_overflow_docker_tag]: https://stackoverflow.com/questions/tagged/docker
[github_issues]: https://github.com/arbory/docker/issues
[github_pull_requests]: https://github.com/arbory/docker/pulls?q=is%3Apr+is%3Aclosed

## What is Arbory

Usefull links:

- [Arbory homepage][arbory_homepage]
- [GitHub][github_arbory_repo]
- [Docker Hub][docker_arbory_repo]

[arbory_homepage]: https://www.arborycms.com/
[github_arbory_repo]: https://github.com/arbory/arbory
[docker_arbory_repo]: https://hub.docker.com/r/arbory/arbory


## Misc

example to build on arm:
```
docker buildx build . --platform linux/amd64 --push -f 8.2/mysql/Dockerfile -t arbory/arbory:8.2-mysql
docker buildx build . --platform linux/amd64 --push -f 8.2/mysql/Dockerfile.dev -t arbory/arbory:8.2-mysql-dev

docker buildx build . --platform linux/amd64 --push -f ci/Dockerfile.php8.3-nodejs20 -t arbory/arbory:ci-php8.3-nodejs20
docker buildx build . --platform linux/amd64 --push -f ci/Dockerfile.php8.4-nodejs22 -t arbory/arbory:ci-php8.4-nodejs22
```
