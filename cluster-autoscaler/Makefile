all: build

TAG?=dev
FLAGS=
ENVVAR=

deps:
	go get github.com/tools/godep

build: clean deps
	$(ENVVAR) godep go build ./...
	$(ENVVAR) godep go build -o cluster-autoscaler 

test-unit: clean deps build
	$(ENVVAR) godep go test --test.short -race ./... $(FLAGS)

release: build

ifndef REGISTRY
    $(error REGISTRY is undefined)
endif
	docker build -t ${REGISTRY}/cluster-autoscaler:${TAG} .
	gcloud docker push ${REGISTRY}/cluster-autoscaler:${TAG}

clean:
	rm -f cluster-autoscaler

.PHONY: all deps build test-unit clean release
