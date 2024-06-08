## HELP LEARNING VIDEO SERIES ##

**CODE REPO:**
- https://github.com/devopsjourney1/helm-webapp

**Youtube video 1. Helm and Helm Charts Explained - Helm Tutorial for Beginners**
- https://www.youtube.com/watch?v=w51lDVuRWuk&list=PLnFWJCugpwfzCjufOk52ufg7CDxpLEmXi

**MAIN POINTS**
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

**Helm Commands**
1. helm repo [Command]      - Repository Management, and listing helm packages (add, list, remove, update)
2. helm install/uninstall   - Install/Uninstall a helm chart (helm install HELM CHART UNIQUE NAME - LOCATION OF HELM CHART CAN BE LOCAL PATH ON THE FILE SYSTEM OR REPO/CHART NAME - INLINE PARAMETERS OR ADDITIONAL VALUE YAML FILES )
3. helm list [flags]        - List out helm releases in your environment (helm list --all-namespaces)
4. helm status [release_name]    - Gives Further Details of a helm installation: revision #, deployment time, current status, etc. (helm status helm-chart-name)
5. helm uninstall [release_name] --keep-history     (--keep-history flag is helpful for rollback)


**Youtube video 2. Helm - Install software in Kubernetes: Practical Tutorial**
- https://www.youtube.com/watch?v=gg-GuHs8Nsk&list=PLnFWJCugpwfzCjufOk52ufg7CDxpLEmXi&index=2

**Youtube video 3. How to Create Helm Charts - The Ultimate Guide**
- https://www.youtube.com/watch?v=jUYNS90nq8U&list=PLnFWJCugpwfzCjufOk52ufg7CDxpLEmXi&index=3

