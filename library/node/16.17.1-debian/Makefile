# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=library
REPOSITORY?=node
TAG?=16.17.1-debian

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
ALIAS = $(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):16.17.1


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
