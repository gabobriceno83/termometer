pipeline {
  agent { label 'Slave_QA2' }
 // agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
  
  tools {
    // Install the Maven version configured as "M3" and add it to the path.
    maven "M3"
   }
   
  stages {
    stage('Build') {
      steps {
         bat 'mvn clean package'
   
      }
    }
    stage('Upload to Artifactory') {
      agent {
        docker {
          image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
          reuseNode true
        }
      }
      steps {
        bat 'jfrog rt upload --url https://pruebaitera.jfrog.io/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/demo-0.0.1-SNAPSHOT.jar java-web-app/'
      }
    }
  }
}
