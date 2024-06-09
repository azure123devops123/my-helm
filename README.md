## HELP LEARNING VIDEO SERIES ##

**CODE REPO:**
- https://github.com/devopsjourney1/helm-webapp

## Youtube video 1. Helm and Helm Charts Explained - Helm Tutorial for Beginners##
- https://www.youtube.com/watch?v=w51lDVuRWuk&list=PLnFWJCugpwfzCjufOk52ufg7CDxpLEmXi

- In this guide I go over the complete theory of how Helm works with Kubernetes and how Helm Charts are used to install software into Kubernetes clusters in the real world.

**IMPORTANT POINTS:**

1. Helm is K8s Package Manager like (brew, apt, dnf) to install application on a server or pc.

2. Helm can be used to INSTALL, UPGRADE and ROLLBACK K8s application.

3. Provides simplification during the complex deployments. Like installations of 'prometheus' using 'helm chart' from 'Artifact Hub'. We don't need to reinvent the wheel.

4. Helm chart is collection of yml files bundled together.

5. Helm chart also use 'TEMPLATING' allowing customization (Dynamic Configuration).

6. Three main components: HELM CHART, CONFIG VALUES and HELM RELEASES.

7. Helm Templating Engine. Define Common Blueprint through helm chart for different environments like (DEV, TEST, PROD) and any dynamic values can be overridden. values.yml, values-dev.yml, values-test.yml, values-prod.yml

8. Directory Structure:   
   - top level directory - NAME OF HELM CHART
   - chart.yaml - META DATA ABOUT THE CHART such as name, description and version
   - templates directory - Helm templated K8s manifest files (deployment.yml, service.yaml etc) + NOTES.txt (deployment notes info will be printed out to the console when run helm install or helm status command)
   - Value configuration files (values.yml, values-dev.yml, values-test.yml, values-prod.yml)
   - Helm V2 (have TILLER service) because used client server model - Helm V3 (don't have TILLER service) because now Helm cli manages all releases directly using K8s api.

**Helm Main Commands:**

1. helm repo [Command]      - Repository Management, and listing helm packages (add, list, remove, update)

2. helm install/uninstall   - Install/Uninstall a helm chart (helm install HELM CHART UNIQUE NAME - LOCATION OF HELM CHART CAN BE LOCAL PATH ON THE FILE SYSTEM OR REPO/CHART NAME - INLINE PARAMETERS OR ADDITIONAL VALUE YAML FILES )

3. helm list [flags]        - List out helm releases in your environment (helm list --all-namespaces)

4. helm status [release_name]    - Gives Further Details of a helm installation: revision #, deployment time, current status, etc. (helm status helm-chart-name)

5. helm uninstall [release_name] --keep-history     (--keep-history flag is helpful for rollback)


## Youtube video 2. Helm - Install software in Kubernetes: Practical Tutorial##
- https://www.youtube.com/watch?v=gg-GuHs8Nsk&list=PLnFWJCugpwfzCjufOk52ufg7CDxpLEmXi&index=2

- In this video I take you over how to get Helm installed and how to deploy applications into your Kubernetes cluster using Helm Charts. We go over how to release, update, rollback and customize Helm Charts. This tutorial is applicable to Mac OS, Windows and Linux.

**Pre-requisite**

1. We must have a k8s cluster up and running (minikube on workstation or any other on linux server)
2. We must installed 'kubectl'

- Minikube Cluster:
    - `minikube start --nodes=1 --profile=local-cluster --driver=docker`

    - `minikube status --profile=local-cluster`     - Minikube cluster is running

**Install Helm CLI Utility**

- On MacOS: 
    - `brew install helm`

    - `helm version`      - Installed Version: v3.15.1

- Prometheus Installation using helm chart: 
  
  1. COMMAND LINE SEARCH: `helm search hub prometheus`      
  
  OR

  2. Search for official 'prometheus' on the WEBSITE: https://artifacthub.io/     Click on install and it will give us two following commands to install it.

    - `helm repo add prometheus-community https://prometheus-community.github.io/helm-charts`   - Add Prometheus Community Repository

    - `helm repo list`          -  Now we have a 'prometheus-community' repo

    - `helm install my-prometheus prometheus-community/prometheus --version 25.21.0`            - Install chart

    - `helm search repo prometheus-community`       - Can see all the packages inside 'prometheus-community' repo

    - `helm install my-prometheus prometheus-community/prometheus --version 25.21.0`

    - `kubectl get all`         - WAIT UNTIL EVERYTHING IS UP AND RUNNING

    - `helm ls --all-namespaces`

    - `helm status my-prometheus`       
    
        - Copy the BOTH COMMANDS so we can get Prometheus server URL like (127.0.0.1:9090)
        - Copy the BOTH COMMANDS so we can get Alertmanager server URL like (127.0.0.1:9093)
        - Copy the BOTH COMMANDS so we can get PushGateway server URL like (127.0.0.1:9091)

- Check releases:
   
    - `helm ls --all-namespaces`    OR      `helm ls -A`
   
- Lets say we want another release into a 'dev' namespace.

   - `kubectl create namespace dev`         - Create a new dev namespace

   - `kubectl get namespaces`               - We can see the 'dev' namespace

   - `helm install my-prometheus-dev prometheus-community/prometheus --version 25.21.0 --namespace dev`

   - `helm ls --all-namespaces`    OR     `helm ls -A`   - We can see one release in a 'default' namespace and one in the 'dev' namespace

- Lets say we want to uninstall helm release into a 'default' namespace.

   - `helm uninstall my-prometheus --keep-history`

   - `helm ls -A`           - Now we have only one release into 'dev' namespace only

   - `helm ls -A -a`        - We can see all the installed and uninstalled releases

- Lets say we want to upgrade helm release into the 'dev' namespace.

   - `helm upgrade my-prometheus-dev prometheus-community/prometheus --version 25.0.0 -n dev`

   - `helm ls -n dev`       - We can see REVISION is 2 and also CHART is 25.0.0

- Lets say we want to rollback our helm release into the 'dev' namespace.

   - `helm history my-prometheus-dev -n dev`        - We can see the whole history of the release in the 'dev'
   
   - `helm rollback my-prometheus-dev 1 -n dev`     - We want ot rollback to revision 1

   - `helm ls -n dev`       - We can see that its the revision 3 but the we successfully rollback to CHART prometheus-25.21.0

   - `helm history my-prometheus-dev -n dev`

**WE CAN SEE THE DETAILED DOCUMENTATION ON THE www.artifacthub.io**

- Cleanup:

   - `helm uninstall my-prometheus-dev --keep-history -n dev` 

## Youtube video 3. How to Create Helm Charts - The Ultimate Guide##

- https://www.youtube.com/watch?v=jUYNS90nq8U&list=PLnFWJCugpwfzCjufOk52ufg7CDxpLEmXi&index=3

- Learn how to create your own Helm Charts! in this video I take you through how you can convert a Kubernetes manifest into a deployable Helm Chart.

**STEP NO. 1 - Start the minikube cluster:**

   - `minikube start`         - Make sure minikube cluster is running

**STEP NO. 2 - Create a helm chart which will create a general scaffolding for us:**

   - `helm create webapp1`          - It will create a directory structure for us

   - `tree webapp1`
         webapp1
         ├── Chart.yaml
         ├── charts
         ├── templates
         │   ├── NOTES.txt
         │   ├── _helpers.tpl
         │   ├── deployment.yaml
         │   ├── hpa.yaml
         │   ├── ingress.yaml
         │   ├── service.yaml
         │   ├── serviceaccount.yaml
         │   └── tests
         │       └── test-connection.yaml
         └── values.yaml

**STEP NO. 3 - Delete unnecessary files and directories from 'templates' directory.**

  - `cd webapp1/templates`

  - `rm -rf ingress.yaml serviceaccount.yaml _helpers.tpl hpa.yaml tests`

  - `cd ../../`

  - `tree webapp`
      webapp1
      ├── Chart.yaml          # name and version will be change in this file
      ├── charts              # If our charts has any dependencies on other charts. We will throw them here
      ├── templates
      │   ├── NOTES.txt
      │   ├── deployment.yaml
      │   └── service.yaml
      └── values.yaml         # This is the default configuration for our helm chart

**STEP NO. 4 - Copy the K8s manifest files into the 'webapp1/templates' directory.**

**Minikube Commands Helping Resource:**

https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fbinary+download#Service

**STEP NO. 5 - Move into the parent directory and then run the following commands to install our chart and then check in the browser:**

  - `helm install mywebapp-release webapp1/`    - 'mywebapp-release' is our release name

  - `kubectl get po -A`               - Wait until everything is up and running

  - `kubectl get all`

  - `kubectl get services`          - Get the service name

  - `minikube service mywebapp`     - minikube launch a web browser -> http://127.0.0.1:51311/hello

  OR

  - `curl localhost:51311/hello`    - We can check in the terminal we can see its returning some traffic.

**STEP NO. 6 - Lets template few things in the service deployment and configmap files and then pass the values.yaml file**

- `helm upgrade mywebapp-release webapp1/ --values webapp1/values.yaml` - Noticed: Release has been upgraded

- `helm ls`          - We can see REVISION is updated to 2

- `kubectl get all`  - All the old pods are terminated and the new pods has been created with the new name. Check the age of the pods.

Lets template the rest of our application and upgrade the release:

- `helm upgrade mywebapp-release webapp1/ --values webapp1/values.yaml` - Noticed: Release has been upgraded

- `helm ls`          - We can see REVISION is updated to 3

- `kubectl get all`  - All the old pods are terminated and the new pods has been created with the new name. Check the age of the pods.

Add the code into NOTES.txt so the user can get the output in the terminal to let the use know how to access the application.

- `helm upgrade mywebapp-release webapp1/ --values webapp1/values.yaml` - Noticed: Release has been upgraded

Copy the both commands from terminal an run them in the terminal and you will see the PORT FORWARDING:
Forwarding from 127.0.0.1:8080 -> 8080

- Check in the browser:     http://127.0.0.1:8080/hello    (WORKING)

OR 

- `curl 127.0.0.1:8080/hello`          (WORKING)

**For different environments create different values-dev.yaml and values-prod.yaml files which will override the default values.yaml**

Create the dev and pod names:

- `kubectl create namespace dev`

- `kubectl create namespace prod`

- `helm install mywebapp-release-dev webapp1/ --values webapp1/values.yaml -f webapp1/values-dev.yaml -n dev`

- `helm install mywebapp-release-prod webapp1/ --values webapp1/values.yaml -f webapp1/values-prod.yaml -n prod`

- `kubectl get all -A`     - Everything is up and running in all the workspaces

- `kubectl get all -n dev`

- `kubectl get all -n prod`

- `helm ls -A -a`

**Now access the web application in the dev and prod environment & make sure we are getting both custom headers for prod and dev environments.**