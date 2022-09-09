
node ('master') {   

  stage ('SCM') { 
    checkout([$class: 'GitSCM', 
       branches: [[name: '*/master']], 
       extensions: [], 
       userRemoteConfigs: [[url: 'https://github.com/ganeshhp/Maven-petclinic-project.git']]])

  }

  stage ('app_build') {
    
      sh 'mvn clean install'
  }
  stage ('plublish_reports') {
    publishHTML([allowMissing: false, 
        alwaysLinkToLastBuild: false, 
        keepAll: false, 
        reportDir: 'target/site/jacoco', 
        reportFiles: 'index.html', 
        reportName: 'Test_reports', reportTitles: ''])
    }
  
  input 'Do you want to Proceed with deployment?'

  stage ('deploy_to_artifactory') {
    sh 'curl -uuser1:APe8TNpyXKCb8VLuunDCEJcab2 -T target/petclinic.war "https://ganeshpalnitkar.jfrog.io/artifactory/Helloworldapp-repo/petclinic.war"'
  }

  stage ('archive') {
    archiveArtifacts artifacts: 'target/petclinic.war', 
       followSymlinks: false
  }

}
