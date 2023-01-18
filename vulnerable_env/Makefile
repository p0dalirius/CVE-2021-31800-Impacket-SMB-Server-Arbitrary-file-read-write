.PHONY: build img

IMGNAME := cve_2021_31800
PORT := 445

all : build start

build:
	docker build -t $(IMGNAME):latest -f Dockerfile .

start: build
	docker run --rm -it -p $(PORT):445 $(IMGNAME)

background:
	docker run --rm -d -p $(PORT):445 $(IMGNAME)

shell:
	docker exec -it $(shell docker ps | grep $(IMGNAME) | awk '{split($$0,a," "); print a[1]}') bash

stop:
	docker stop $(shell docker ps | grep $(IMGNAME) | awk '{split($$0,a," "); print a[1]}')