/* This file was written by reffering bookmarked link named "Declarative pipeline Documentation" */

/* content which is inside the steps (written in Jenkins DSL) is not given in documentation. Hence, we write it referring 
the snippet generator of scripted pipeline. Therefore, the content inside the steps is the same as in scripted pipeline's
Jenkinsfile. The only difference between declarative & scripted pipeline script is just the external body, inside, it's 
all Jenkins DSL */

pipeline {
    agent { label 'node-1' } 
    stages {
        stage('git') {
            steps { 
                git branch: 'declarative', url: 'https://github.com/Adithya119/java11-examples.git'
            }
        }
        stage('build') {
            steps {
                sh '/usr/local/apache-maven-3.8.7/bin/mvn clean package'
            }
        }
        stage('archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
        stage('test results') {
            steps {
                junit '**/TEST-*.xml'
            }
        }
    }

}