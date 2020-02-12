all: build
IMG=oprid/php-fpm
VER=7.4
build:
	@docker build -t ${IMG}:${VER} -f Dockerfile ../..
	@docker tag ${IMG}:${VER} ${IMG}:latest

push:
	@docker push ${IMG}:${VER}
	@docker push ${IMG}:latest
