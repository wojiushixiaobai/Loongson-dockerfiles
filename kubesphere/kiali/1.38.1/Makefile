# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=kubesphere
REPOSITORY?=kiali
TAG?=1.38.1

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)


default: image

download: clean
	wget "https://github.com/Loongson-Cloud-Community/kiali/releases/download/v1.38.1/kiali"
	chmod +x kiali

image: download
	docker build \
		-t $(IMAGE) \
		.

push:
	docker push $(IMAGE)

clean:
	rm -f kiali
