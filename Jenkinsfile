pipeline {
agent { label 'Slave_Dev1' }
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
    maven "MAVEN"
    jdk 'Java8'
   }
   
  stages {
    stage('Compilacion') {
      steps {
         bat 'mvn clean package'
   
      }
    }
    
    stage('UPLOAD-ARTECTORY') {
      steps {
     powershell """("Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf v2.24.2/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT\\system32\\jf.exe'")"""
     
     bat'jf rt u --url http://192.168.0.60:8082/artifactory --access-token %ARTIFACTORY_ACCESS_TOKEN% target/termometer-0.0.1-SNAPSHOT.jar java-web-app/'
     
     bat'jf rt dl "java-web-app/target/termometer-0.0.1-SNAPSHOT.jar" --url http://192.168.0.60:8082/artifactory --access-token %ARTIFACTORY_ACCESS_TOKEN% C:\\compilado\\'
        }
  
      }   
  
  }
  
}
