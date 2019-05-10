node ('master') {

checkout([$class: 'GitSCM', 
   branches: [[name: '*/master']], 
   doGenerateSubmoduleConfigurations: false, 
   extensions: [], 
   submoduleCfg: [], 
   userRemoteConfigs: [[url: 'https://github.com/ganeshhp/Maven-petclinic-project.git']]])
   
bat label: '', script: 'mvn clean package'   

archiveArtifacts 'target/*.war'

}

