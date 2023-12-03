pipeline {
  agent {
    kubernetes {
      label 'sample-app'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  containers:
  - name: gcloud-kubectl-docker
    image: gcr.io/disco-domain-402111/gcloud-kubectl-docker
    command:
    - cat
    tty: true
"""
}
  }
  stages {
    stage('Build and push image with Container Builder') {
      steps {
        container('gcloud') {
          sh "docker build ."
          sh "PYTHONUNBUFFERED=1 gcloud builds submit -t gcr.io/disco-domain-402111/adservice1 ."
        }
      }
   }
}
}
