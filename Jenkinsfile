

pipeline {
    agent any

    parameters {
        choice(
            name: 'executeJob',
            choices: ['Yes', 'No'],
            description: 'Do you want to execute the job?'
        )
    }

    stages {
        stage('git cloned') {
            steps {
                git url:'https://github.com/sushant960kr/php-project/', branch: "master"
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    sh 'docker build -t sushant960kr/newimage .'
                    sh 'docker images'
                }
            }
        }
        stage('Docker login') {
            when {
                expression { params.executeJob == 'Yes' }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push sushant960kr/newimage'
                }
            }
        }
        stage('Deploy') {
            when {
                expression { params.executeJob == 'Yes' }
            }
            steps {
                script {
                    def dockerrm = 'sudo docker rm -f My-first-containe221 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 sushant960kr/newimage'
                    sshagent(['sshkeypair']) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.9.161 ${dockerrm}"
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.9.161 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
