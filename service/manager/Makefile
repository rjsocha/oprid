all: build
IMG=oprid/manager
VER=1.0
build:
	@docker build -t ${IMG}:${VER} -f Dockerfile ..
	@docker tag ${IMG}:${VER} ${IMG}:latest

push:
	@docker push ${IMG}:${VER}
	@docker push ${IMG}:latest

