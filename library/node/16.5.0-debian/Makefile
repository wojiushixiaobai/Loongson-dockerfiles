# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=library
REPOSITORY?=node
TAG?=16.5.0-debian

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
ALIAS = $(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):16.5.0

default: image

image:
	docker build \
		-t $(IMAGE) \
		.

push: alias
	docker push $(IMAGE)
	docker push $(ALIAS)

alias:
	docker tag $(IMAGE) $(ALIAS)
