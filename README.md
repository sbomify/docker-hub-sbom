# Docker Hub SBOMs

This GitHub Actions workflow runs a specified command on a set of Docker images and generates Software Bill of Materials (SBOMs) in CycloneDX and SPDX formats for each image. The workflow is scheduled to run every night at midnight UTC.

## Build the List

To get the top 15 (official) Docker Hub repositories, use the following command:

```bash
curl -s "https://hub.docker.com/v2/repositories/library/?page_size=100" | \
    jq -r '.results[] | "\(.pull_count) \(.name)"' | \
    sort -nr | \
    head -n 15
```

Currently, this yields the following images:

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

Note: We're only checking the `:latest` tag to avoid iterating over every tag combination.

## Generating SBOMs

Every night, the workflow pulls the latest Docker images and generates SBOMs in both CycloneDX and SPDX formats using [Syft](https://github.com/anchore/syft).
