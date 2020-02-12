IMG=oprid/nginx
VER=1.0

all: build

build:
	@docker build -t ${IMG}:${VER} -f Dockerfile ..
	@docker tag ${IMG}:${VER} ${IMG}:latest

push:
	@docker push ${IMG}:${VER}
	@docker push ${IMG}:latest
