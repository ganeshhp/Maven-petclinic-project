pipeline {
 agent none
    stages {
      stage('SCM_Chekout') {
          agent { label "master" }
	steps {
	                checkout([$class: 'GitSCM',
                	    branches: [[name: '*/master']],
                    	   doGenerateSubmoduleConfigurations: false,
                    	   extensions: [],
                     	   submoduleCfg: [],
                    	   userRemoteConfigs: [[url: 'https://github.com/ganeshhp/Maven-petclinic-project.git']]])
            }
        }
     stage('code-validation') {
         agent { label "master" }
	steps {
                       sh 'mvn -f pom.xml sonar:sonar'
            }
        }
     stage('Test and package'){
          agent { label "master" }
	steps {
                      sh 'mvn -f pom.xml package'
            }
        }

}
}
