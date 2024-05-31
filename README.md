# Docker Hub SBOMs

Generate the SBOMs for the top 15 Docker Hub repositories.

## Build the list

We can get the top 15 (official) Docker Hub repositories from the API as follows:

```bash
$ curl -s "https://hub.docker.com/v2/repositories/library/?page_size=100" | \
    jq -r '.results[] | "\(.pull_count) \(.name)"' | \
    sort -nr | \
    head -n 15
```

That currently gives us the following images:

* nginx
* memcached
* busybox
* alpine
* ubuntu
* redis
* postgres
* python
* node
* httpd
* mongo
* mysql
* rabbitmq
* docker
* hello-world

