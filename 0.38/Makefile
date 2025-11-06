VERSION = 0.38
VERSION2 = 0.38.1
DOCKER_REPO = trimmomatic

SHORT_HASH := $(shell git rev-parse --short HEAD)
DOCKER_URL := quay.io/ncigdc
DOCKER_IMAGE := ${DOCKER_URL}/${DOCKER_REPO}:${VERSION2}
DOCKER_IMAGE_HASH := ${DOCKER_URL}/${DOCKER_REPO}:${VERSION}-${SHORT_HASH}

.PHONY: version version-* name
name:
	@echo ${NAME}

version:
	@echo --- VERSION: ${VERSION2} ---

version-docker:
	@echo ${DOCKER_IMAGE_COMMIT}
	@echo ${DOCKER_IMAGE}

.PHONY: docker-*
docker-login:
	@echo
	docker login -u=${QUAY_USERNAME} -p=${QUAY_PASSWORD} quay.io

.PHONY: build build-*
build: build-docker

build-docker:
	@echo
	@echo -- Building docker --
	docker build . \
		--file ./Dockerfile \
		--build-arg VERSION=${VERSION2} \
		-t "${DOCKER_IMAGE}" \
		-t "${DOCKER_IMAGE_HASH}"

.PHONY: publish
publish: docker-login
	docker push ${DOCKER_IMAGE}
	docker push ${DOCKER_IMAGE_HASH}
