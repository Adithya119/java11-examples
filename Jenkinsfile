node('node-1') {
    properties([pipelineTriggers([upstream('starter,')])])
    stage('git') {
      git branch: 'scripted', url: 'https://github.com/Adithya119/java11-examples.git'
	stage('build') {
      sh '/usr/local/apache-maven-3.8.7/bin/mvn clean package'
	stage('arhcive') {
      archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
	stage('publish test results') {
      junit '**/TEST-*.xml'
}
}
}
}
}