pipeline {
   agent any

   environment {
     // You must set the following environment variables
     // ORGANIZATION_NAME
     // YOUR_DOCKERHUB_USERNAME (it doesn't matter if you don't have one)
     
     SERVICE_NAME = "sample-microservice"
     REPOSITORY_TAG="${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
     registry="yasha192/${REPOSITORY_TAG}"
   }
   
   
   stages {
     
      stage('Preparation') {
         steps {
            cleanWs()
            git 'https://github.com/yash-demo/microservice.git'
         }
      }
      
     stage('Permission') {
          steps {
            sh 'chmod +x ./gradlew'
          }
      }
      stage('Build Jar') {
          steps {
            sh './gradlew build'
          }
      }
      stage('Publish') {
           environment {
               registryCredential = 'dockerhub'
           }
           steps{
               script {
                   def appimage = docker.build registry + ":$BUILD_ID"
                   docker.withRegistry( '', registryCredential ) {
                       appimage.push()
                       appimage.push('latest')
                   }
               }
           }
       }

      stage('Deploy to Cluster') {
          steps {
            sh 'kubectl apply -f gradle.yaml'
             sh 'kubectl set image deployments/gradle-deployment gradle-deployment=${REPOSITORY_TAG} -n jenkins'
          }
      }
   }
}
