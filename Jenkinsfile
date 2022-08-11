pipeline {
agent { label 'Slave_Dev1' }
// agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token2')
  }
  
  tools {
    // Install the Maven version configured as "M3" and add it to the path.
    maven "MAVEN"
    jdk 'Java8'
   }
   
  stages {
    stage('Build') {
      steps {
         bat 'mvn clean package'
   
      }
    }
    
    
    stage('JFROG-CLI') {
      steps {
     powershell """("Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf v2.24.2/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT\\system32\\jf.exe'";
     jf rt u --url http://192.168.0.60:8082/artifactory --access-token %ARTIFACTORY_ACCESS_TOKEN% target/termometer-0.0.1-SNAPSHOT.jar java-web-app/)"""
    
    
    //powershell """(
     // bat 'pwsh --version'
    
    //  @powershell "Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2:2.20.0/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT\system32\jf.exe'"
   //powershell script: powershell "Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/[RELEASE]/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT\system32\jf.exe'" ; jf setup
    //echo 'Process Deploy'
       // powershell script: "Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2:2.20.0/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT/system32/jf.exe'"
     //bat 'powershell "Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/[RELEASE]/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT\system32\jf.exe'" ; jf setup'
       //   powershell script:"Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/[RELEASE]/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT\system32\jf.exe'" ; jf setup
    //echo 'Process Deploy'
      } 
    }  
    
  //  stage('Upload') {
   //   steps {
       // powershell script: "Start-Process -Wait -Verb RunAs powershell '-NoProfile iwr https://releases.jfrog.io/artifactory/jfrog-cli/v2:2.20.0/jfrog-cli-windows-amd64/jf.exe -OutFile $env:SYSTEMROOT/system32/jf.exe'"
    // bat 'jf rt u --url http://192.168.0.60:8082/ui/login/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/termometer-0.0.1-SNAPSHOT.jar java-web-app/'
      //  bat 'jf rt u --url http://192.168.0.60:8082/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/termometer-0.0.1-SNAPSHOT.jar java-web-app/'
     
   
   //   } 
  //  }
   
  }
  
}
