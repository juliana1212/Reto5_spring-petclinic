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

    stage('Docker Push') {
      agent any
      environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
      }
      steps {
        echo 'Iniciando sesión en Docker Hub...'
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        echo 'Subiendo imagen al repositorio remoto...'
        sh 'docker push julianacasas28/spring-petclinic:latest'
      }
    }

  }
}
