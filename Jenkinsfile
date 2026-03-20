pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'JAVA21'
    }
    stages {
        stage('Download Code') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/chauhangaurav192/maven-jenkins-gaurav.git']])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Generate Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Trigger Deploy Pipeline')
         {
            steps 
            {
                build wait: false, job: 'deploy-pipeline'
            }
        }        
    }
}
