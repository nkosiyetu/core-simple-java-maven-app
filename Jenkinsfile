pipeline {
  agent {
    kubernetes {
      label 'maven-pod-template'
      defaultContainer 'maven-container'
      yamlFile 'KubernetesJDK11.yaml'
    }
  }
  stages {
    stage('JDK 11 Build & Test') {
      steps {
        container('maven-container-jdk-11') {
          sh 'mvn --version'
          sh 'mvn -B clean package'
        }
      }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
      post {
        always { 
          junit '**/*.xml'
        }
      }
    }
    stage('Deliver') {
      steps {
        sh 'jenkins/scripts/deliver.sh'
      }
    }
  }
}
