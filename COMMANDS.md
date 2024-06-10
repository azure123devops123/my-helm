## :smile: MacOSX Installation: ##

1. K8s cluster up and running (Pre-requisite):

         minikube start

         minikube status

2. K8s CLI (kubectl) must installed (Pre-requisite):

         brew install kubectl

         kubectl version --client

3. Helm CLI (kubectl) must installed

         brew install helm

         helm version

## :smile: Basic Commands for downloading and installing helm chart of **prometheus stack** from artifacthub: ##

         helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

         helm repo list

         kubectl create namespace dev

         kubectl get namespaces

         helm install my-prometheus-dev prometheus-community/prometheus --version 25.0.0 -n dev

         kubectl get all -n dev

         helm ls -n dev

         helm ls --all-namespaces    OR      helm ls -A    OR      helm ls -a -A

         helm status my-prometheus-dev -n dev

         helm upgrade my-prometheus-dev prometheus-community/prometheus --version 25.21.0 -n dev

         helm history my-prometheus-dev -n dev

         helm rollback my-prometheus-dev 1 -n dev

         helm uninstall my-prometheus-dev --keep-history -n dev

## :smile: Basic Commands for creating chart of your web application and deploy using helm: ##

         helm create webapp1

         tree webapp1    # REMOVE UNNECESSARY FILES AND DIRECTORIES + ADD YOUR MANIFESTS FILES + EDIT NOTES.txt FILE

         helm install mywebapp-release webapp1/

         kubectl get all

         minikube service mywebapp

         curl localhost:51311/hello

## :smile: Basic Commands for templating your web application: ##

      # Test the rendering of our template

      // Test the rendering of our template

      helm template mywebapp-release webapp1

      helm upgrade mywebapp-release webapp1/ --values webapp1/values.yaml

## :smile: Basic Commands for templating your web application for different environments (dev, prod):

      kubectl create namespace dev

      helm install mywebapp-release-dev webapp1/ --values webapp1/values.yaml -f webapp1/values-dev.yaml -n dev



