/new declarative syntax used
pipeline {
 agent none
    stages {
      stage('SCM_Chekout') {
          agent { label 'master' }
	steps {
	  checkout([$class: 'GitSCM', 
          branches: [[name: '*/master']], 
          doGenerateSubmoduleConfigurations: false, 
          userRemoteConfigs: [[url: 'https://github.com/ganeshhp/Maven-petclinic-project.git']]])
            }
        }
parallel {
     stage('code-validation') {
         agent { label "master" }
	steps {
                       bat 'mvn -f pom.xml sonar:sonar'
            }
        }
     stage('Test and package') {
          agent { label "master" }
	steps {
                      bat 'mvn -f pom.xml package'
        }
      }
    }
  }
}
