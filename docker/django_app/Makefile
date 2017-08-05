.PHONY: build push
#GIT_TAG_NAME ?=$(shell git tag -l --contains HEAD | tail -n1)
GIT_VERSION ?= $(shell git rev-parse HEAD)
BUILD_DATE := $(shell date +'%Y-%m-%dT%H:%M:%SZ')
IMAGE_NAME := djangoapp
DOCKER_REGISTERY := mozuffer
IMAGE_VERSION =latest
all: push
# Build Docker Image with Build Number and Latest tag
build:
	docker build -t $(DOCKER_REGISTERY)/$(IMAGE_NAME):$(IMAGE_VERSION) .

         # push docker images to docker registry
push: build
	docker push $(DOCKER_REGISTERY)/$(IMAGE_NAME):$(IMAGE_VERSION)
