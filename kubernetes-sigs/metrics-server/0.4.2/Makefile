# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=kubernetes-sigs
REPOSITORY?=metrics-server
TAG?=0.4.2

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)

METRICS_REPOSITRY?=https://github.com/kubernetes-sigs/metrics-server.git

default: image

cmd: 
	git clone --branch v$(TAG) --depth=1 $(METRICS_REPOSITRY)
	mv metrics-server/cmd .
	mv metrics-server/pkg .
	mv metrics-server/go.mod .
	rm -rf metrics-server/

download: cmd

image: download
	docker build \
		-t $(IMAGE) \
		.

push:
	docker push $(IMAGE)
