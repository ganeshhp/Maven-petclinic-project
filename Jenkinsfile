
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
  
        input 'proceed with artifact upload?'
        
  stage ('artifact-repo'){
    sh 'curl -uuser1:AP2tXv3LMf5WVPWuRUdGVHCCa4B -T target/petclinic.war "https://pluforum.jfrog.io/artifactory/webapp-sample/petclinic.war"'
  }
  
  stage ('archive') {
    archiveArtifacts artifacts: 'target/petclinic.war', followSymlinks: false
  }
}
