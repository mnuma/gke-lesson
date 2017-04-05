.PHONY: help

help: ## show help.
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

gcloud-create-clusters-development: ## gcloud-create-clusters-development.
	@gcloud container clusters create c1 \
    --num-nodes 2 \
    --machine-type g1-small
	@gcloud config set container/cluster c1
	@gcloud container clusters get-credentials c1

gcloud-create-clusters-describe: ## gcloud-create-clusters-describe.
	@gcloud container clusters describe ${TARGET}

kubectl-create-deployment: ## kubectl create deployment.
	@kubectl create -f ./nginx-deployment.yaml --record
	@kubectl get deployments

kubectl-create-service: ## kubectl create service.
	@kubectl create -f ./nginx-service.yaml --record
	@kubectl get deployments

kubectl-get: ## kubectl get.
	@echo "-------------------------------------------------"
	@echo "show deployments"
	@echo "-------------------------------------------------"
	kubectl get deployments
	@echo "-------------------------------------------------"
	@echo "show rs"
	@echo "-------------------------------------------------"
	kubectl get rs
	@echo "-------------------------------------------------"
	@echo "show services"
	@echo "-------------------------------------------------"
	kubectl get services
	@echo "-------------------------------------------------"
	@echo "show pods"
	@echo "-------------------------------------------------"
	kubectl get pods --show-labels -o wide

kubectl-set-image: ## kubectl set image
	kubectl set image deployment/nginx-deployment nginx=${NGINX}
	kubectl get rs
	kubectl get pods --show-labels -o wide

pod-ssh: ## pod ssh
	@kubectl exec -it ${TARGET} /bin/bash
