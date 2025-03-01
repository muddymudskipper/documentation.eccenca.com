---
title: "cmemc: Using the Docker Image"
icon: material/docker
tags:
  - Docker
  - cmemc
---
# Using the Docker Image

## Introduction

In addition to the cmemc distribution package, you can use the eccenca cmemc docker image which is based on the official [debian slim image](https://hub.docker.com/_/debian).
This is especially needed if you want to use cmemc in orchestrations.

## Image and Tags

The following image - tag combinations are available for public use:

- `docker-registry.eccenca.com/eccenca-cmemc:v22.1` - a specific release
- `docker-registry.eccenca.com/eccenca-cmemc:latest` - same as the latest release

``` shell-session title="Image retrieval and check cmemc version"
$ docker run -it --rm docker-registry.eccenca.com/eccenca-cmemc:v22.1 --version
Unable to find image 'docker-registry.eccenca.com/eccenca-cmemc:v22.1' locally
v22.1: Pulling from eccenca-cmemc
Digest: sha256:29bdd320e02f1b7758df22528740964225b62530c73c773a55c36c0e9e18b647
Status: Downloaded newer image for docker-registry.eccenca.com/eccenca-cmemc:v22.1
cmemc, version v22.1.1, running under python 3.9.13
```

## Volumes

cmemc processes a configuration file and can import and export files which represent graph, project or workspace payloads.
These files need to be mounted via [docker volumes](https://docs.docker.com/storage/volumes/) to be accessible for the dockerized cmemc.

- `/config/cmemc.ini` (file) - the loaded configuration file
- `/data` (directory) - the working directory

``` shell-session title="Using a volume to mount the config."
$ cat cmemc.ini
[my-deployment]
CMEM_BASE_URI=https://data.example.org/
OAUTH_GRANT_TYPE=client_credentials
OAUTH_CLIENT_ID=cmem-service-account
OAUTH_CLIENT_SECRET=credentialshere

$ docker run -it --rm -v "$(pwd)"/cmemc.ini:/config/cmemc.ini docker-registry.eccenca.com/eccenca-cmemc:v22.1 config list
my-deployment
```

``` shell-session title="Using a volume to additionally mount the data directory."
$ cat list-graphs.sparql
SELECT DISTINCT ?graph (COUNT(?graph) AS ?triples)
WHERE {
    GRAPH ?graph
    {
        ?s ?p ?o
    }
}
GROUP BY ?graph
ORDER BY DESC(?triples)

$ docker run -it --rm -v $(pwd):/data -v $(pwd)/cmemc.ini:/config/cmemc.ini docker-registry.eccenca.com/eccenca-cmemc:v22.1 -c my-deployment query execute ./list-graphs.sparql
graph,triples
http://schema.org/,8809
https://vocab.eccenca.com/shacl/,1752
[...]
```

