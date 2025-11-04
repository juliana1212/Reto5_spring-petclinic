pipeline {
  agent none
  stages {

    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3.9-eclipse-temurin-25'
          reuseNode true
        }
      }
      steps {
        sh 'mvn clean install'
      }
    }

    stage('Docker Build') {
      agent any
      steps {
        echo 'Construyendo imagen Docker...'
        sh 'docker build -t julianacasas28/spring-petclinic:latest .'
      }
    }

  }
}
