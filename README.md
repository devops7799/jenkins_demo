# jenkins_demo
Objects in this repo are used to deploy a Jenkins server on K8 cluster. And create docker image using a Jenkinsfile.

# References:
https://www.jenkins.io/doc/book/installing/kubernetes/


# Pre-requisite steps:
1. Create PV for storing Jenkins data:-
   - kubectl apply -f jenkins-volume.yaml
2. Create service account and configure RBAC for jenkins:-
   - kubectl apply -f jenkins-sa.yaml
3. Update jenkins-values.yaml that will be used for deploying the jenkins helm chart:-

# Helm chart deployment:
- helm repo add jenkinsci https://charts.jenkins.io
- helm repo update
- helm install jenkins -n jenkins -f jenkins-values.yaml jenkinsci/jenkins

NOTES:
1. Get your 'admin' user password by running:-
   - kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/chart-admin-password && echo
2. Get the Jenkins URL to visit by running these commands in the same shell:-
   - echo http://127.0.0.1:8080
   - kubectl --namespace jenkins port-forward svc/jenkins 8080:8080
3. Login with the password from step 1 and the username: admin

# Dockerfile
- This is used for building the docker image for using sample.war

# Jenkinsfile
- Ref:https://www.jenkins.io/doc/book/pipeline/getting-started/#defining-a-pipeline-in-scm
- Pipeline stages are defined in this file which will build the docker image and push to the docker repo.

