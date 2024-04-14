VERSION=0.1.1

integrate: clean build push

clean:
	rm -rf node_modules
	rm -rf dist

build:
	docker build . --progress=plain -f Dockerfile -t ghcr.io/wilsonify/rockstar-sre-node-api:${VERSION} --label "org.opencontainers.image.source=https://github.com/wilsonify/rockstar-sre"

stop:
	docker stop node-api || true

run: build stop
	docker run --rm --name node-api -p 32769:8080 ghcr.io/wilsonify/rockstar-sre-node-api:${VERSION}

healthcheck:
	curl -f http://localhost:32769/health

push:
	docker push ghcr.io/wilsonify/rockstar-sre-node-api:$VERSION

deploy:
	# Microservices App - create a deployment with replicaset
	kubectl create -f k8s/node-api-deployment.yaml
	# Microservices App - expose app listener port as a service
	kubectl create -f k8s/node-api-service.yaml
	# Microservices App - create an external load balancer for the service
	kubectl create -f k8s/node-api-lb-service.yaml





