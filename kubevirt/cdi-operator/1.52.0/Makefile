# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=kubevirt
REPOSITORY?=cdi-operator
TAG?=1.52.0
LATEST?=true

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
LATEST_IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):latest

default: image

download:
	wget https://github.com/Loongson-Cloud-Community/containerized-data-importer/releases/download/v1.52.0/cdi-operator
	wget https://github.com/Loongson-Cloud-Community/containerized-data-importer/releases/download/v1.52.0/csv-generator
	chmod +x cdi-operator csv-generator

image: download
	docker build \
		-t $(IMAGE) \
		.

push:
	docker push $(IMAGE)
	#latest image
	@if [ $(LATEST) = "true" ]; \
		then \
		docker tag $(IMAGE) $(LATEST_IMAGE); \
		docker push $(LATEST_IMAGE); \
	fi
