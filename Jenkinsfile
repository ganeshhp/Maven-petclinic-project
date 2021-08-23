
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
    sh 'curl -uuser1:AP2tXv3LMf5WVPWuRUdGVHCCa4B -T target/petclinic.war "https://pluforum.jfrog.io/artifactory/webapp-sample/petclinic.war"'
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
