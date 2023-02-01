node('node-1') {
    /* properties([pipelineTriggers([upstream('starter,')])]) */   /* properties block mentioning the upsteam to look for */
    try {
      properties([parameters([choice(choices: ['uat', 'scripted', 'master', 'declarative'], description: 'choose a branch to build', name: 'BRANCH_TO_BUILD'), string(defaultValue: 'clean package', description: 'specify the maven goal(s)', name: 'MAVEN_GOAL')]), pipelineTriggers([cron('H */3 * * 0,6'), pollSCM('H/10 * * * *')])])  /* you can also use 0 in the place of H */   /* periodical build + pollSCM + parameters*/
      stage('git') {
        git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/Adithya119/java11-examples.git'
        }
	  stage('build') {
        sh "/usr/local/apache-maven-3.8.7/bin/mvn ${params.MAVEN_GOAL}"
        }
	  stage('arhcive') {
        archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
        }
	  stage('publish test results') {
        junit '**/TEST-*.xml'
        }
      currentBuild.result = 'SUCCESS'
    }

    catch (err) {
        currentBuild.result = 'FAILIURE'
    }

    finally {
        mail to: 'arkariveda@gmail.com',
        subject: "Status of the pipeline: ${currentBuild.fullDisplayName}",
        body: "${env.BUILD_URL} has result ${currentBuild.result}" 
    }
}

/* included all the script inside the "try" block --> notes in the book. */