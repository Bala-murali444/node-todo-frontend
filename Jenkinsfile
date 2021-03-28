pipeline {
  environment {

    registry = "9885614249/todo-app-pipeline"

    registryCredential = 'docker-hub-2'

    dockerImage = ''

  }

  agent any
    
  tools {nodejs "NodeJS"}
    
  stages {
        
    stage('Cloning Git') {
      steps {
        git credentialsId: 'project-1', url: 'https://github.com/Bala-murali444/node-todo-frontend.git'
      }
    }
        
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {

      steps{

        script {

          docker.withRegistry( '', registryCredential ) {

            dockerImage.push()

          }

        }

      }

    }     
    stage('Test') {
      steps {
         sh 'npm test'
      }
    }      
  }
}