# Kubectl commands

## Kubect get [service]
Kubectl get nodes

Kubectl get pod

Kubectl get services

Kubectl get deployment

kubectl get replicaset

kubectl get namespaces

kubectl get all

#### To get yaml file info including status
kubectl get deployment nginx-deployment -o yaml

#### To get more Information like ip
Kubectl get pod -o wide

## Kubectl create

kubectl create deployment nginx-delp --image=nginx

kubectl create deployment mongo-depl --image=mongo

kubectl create namespace [namespace-name]

## Kubectl edit

kubectl edit deployment nginx-dept

## Kubectl logs

kubectl logs mongo-depl-558475c797-9b96k

## Kubectl describe

kubectl describe pod mongo-depl-558475c797-9b96k

## Kubectl exec
kubectl exec-it [pod name]  --  bin/bash

kubectl exec -it mongo-depl-558475c797-9b96k -- bin/bash

## Kubectl delete

kubectl delete deployment mongo-depl

## Kubectl apply
kubectl apply -f config-file.yaml

kubectl apply -f mongo-secret.yaml

kubectl apply -f mongo-deployment.yaml


## To start Load balancer Service
minikube service mongo-express-service

## kubectl apply
kubectl apply -f config-file.yaml —namespace=my-namespace

## Use cases Namespaces:
- Structure your components
- Avoid conflicts between teams
- Share services between different environments 
- Access and Resource Limits on Namespace Level

## ConfigMap & Secret can’t be shared between Namespaces

kubectl api-resources --namespaced=false

## Kubectx & Kubens
### kubectx is a tool to switch between contexts (clusters) on kubectl faster.
### kubens is a tool to switch between Kubernetes namespaces (and configure them for kubectl) easily.

brew install kubectx

kubens (to all namespaces and default selected namespace)

kubens [namespace-name] (this will change the default namespace to [namespace-name])

## Ingress
Install Ingress using Minikube: minikube addons enable ingress

Verify if ingress controller is running: kubectl get pods -n ingress-nginx

Ingress can also be used to set TLS certificate

Volume and Node can’t be created within Namespace

# Helm

Helm file structure:
- Helm charts: bundle of yaml files
- Template Engine: 
    - Define a common blueprint
    - Dynamic values are replaced by placeholders
    - name: {{ .Values.name }}
- Same app across different environments 
- Structure
    - mychart/
        - Chart.yaml   -> Contains meta data about the mychart
        - values.yaml -> default values applies to template
        - charts/        ->  contains all dependencies
        - templates/
        - …

helm create [chart-name]

helm install [release-name] [chart-main-folder-path]

helm install -f [custom-value.yaml] [release-name] [chart-main-folder-path]
- Two ways to pass configuration data during install
    - --values or -f
    - --set: overrides other values

helm install --debug --dry-run [release-name] [chart-main-folder-path]

helm status [release-name]

helm show values [chart-name]

helm upgrade

helm rollback

helm uninstall

helm list --all

helm lint

helm package [file-name-path]



