
node ('master') {

  stage ('SCM') {
    checkout changelog: false, 
        poll: false, 
        scm: [$class: 'GitSCM', 
        branches: [[name: '*/master']], 
        extensions: [], 
        userRemoteConfigs: [[url: 'https://github.com/ganeshhp/Maven-petclinic-project.git']]]
  }
  
  stage ('build') {
    sh 'mvn clean package'
  }
  
  stage ('artifact-repo'){   
    sh 'curl -uuser1:APEkqK6UcRQmCrj4AeR2DMkoMe -T target/petclinic.war "https://autofact.jfrog.io/artifactory/petclinic/petclinic.war"'
  }

  input 'proceed with artifact upload?'
  
  stage ('publish_reports') {
    publishHTML([allowMissing: false, 
         alwaysLinkToLastBuild: false, keepAll: false, 
         reportDir: 'target/site/jacoco', 
         reportFiles: 'index.html', reportName: 'HTML Report', 
         reportTitles: 'test_report'])
  }
  stage ('archive') {
    archiveArtifacts artifacts: 'target/petclinic.war', followSymlinks: false
  }
}
