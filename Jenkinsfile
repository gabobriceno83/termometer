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
    stage('version') {
      steps {
       // powershell script: "Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2:2.20.0/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT/system32/jf.exe'"
        bat 'jfrog rt upload --url https://pruebaitera.jfrog.io/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/demo-0.0.1-SNAPSHOT.jar java-web-app/'
      } 
    }
   
  }
  
}
