# container-ubuntu

## Introduction

Container to mirror apt repositories, based on ubuntu 20.04

## Building the image

A makefile that builds the docker container is included, to build run:

```
NAME="apt-mirror" TAG="latest" make build
```

This will result in a local image tagged with as "apt-mirror:latest".  
See the 'Additional Options' section for more information about the available options.  

To push the image to the repository use the command below.  

## Pushing the image to a repository

The included makefile can also push the build image, first the container is build with the given options and once build it is pushed to the repository.

To build and push, run:

```
NAME="apt-mirror" TAG="latest" make push
```

### Additional Options

There are several options that can be passed to customize the build process.  
The defaults are only set when using the Jenkins pipeline.

- REPO(default: registry.crazyzone.be): repository to push the image to
- NAME(default: apt-mirror): name of the image

The tags used when pushing the image are 'latest' when building the master/main branch and the version set in the VERSION file.

## Using the image

The container expects a sources.list and mirrors.list file to be mounted on their default location.

Example:

```
docker run --rm -ti -v "/tmp/apt-mirror:/mnt/apt-mirror" -v `pwd`"/lib/sources.list:/etc/apt/sources.list" -v `pwd`"/lib/mirror.list:/etc/apt/mirror.list" "registry.crazyzone.be/apt-mirror" "apt-mirror"
```

The location the mirror is downloaded to can be modified in the mirror.list

## Building with Jenkins

The included Jenkinsfile is made to be run and deploy on the crazyzone network.  
The Jenkinsfile can be modified can be modified to apply to other environments