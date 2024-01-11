// node {
//        stage('Build') {
//            docker.image('node:20.10.0-alpine3.19').inside('-p 3000:3000') {
//            sh 'npm install'
//            }
//        }
//        stage('Test') {
//         docker.image('node:20.10.0-alpine3.19').inside('-p 3000:3000') {
//             sh './jenkins/scripts/test.sh'
//             }
//        }  
// }

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
        stage('Deploy') {
            steps {
                input(message: 'Lanjutkan ke tahap Deploy?', submitter: 'user1,user2', submitterParameter: 'APPROVE')
                sh './jenkins/scripts/deliver.sh'
                sh 'sleep 60'
                sh 'chmod +x ./jenkins/scripts/github-pages.sh && ./jenkins/scripts/github-pages.sh'
            }
        }
    }
}




// pipeline {
//     agent {
//         docker {
//             image 'node:20.10.0-alpine3.19'
//             args '-p 3000:3000' 
//         }
//     }
//     stages {
//         stage('Build') { 
//             steps {
//                 sh 'npm install'
//             }
//         }
//     }
//        stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
// }