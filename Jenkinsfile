pipeline {
    agent {
        docker {
            image 'timbru31/node-alpine-git:16'
            args '-p 3000:3000'
        }
    }
    environment {
        GITHUB_TOKEN     = credentials('jenkins-github-token')
        GITHUB_REPOSITORY = 'NovianIR/a428-cicd-labs'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') { 
            steps {
               input(message: 'Lanjutkan ke tahap Deploy?', submitter: 'user1,user2', submitterParameter: 'APPROVE')
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sh 'sleep 60'
                sh 'chmod +x ./jenkins/scripts/github-page && ./jenkins/scripts/github-page'
            }
        }
    }
}