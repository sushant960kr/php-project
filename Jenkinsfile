pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'sushant960kr/sushantnewimage:v1'
        CONTAINER_NAME = 'php-container'
        SSH_OPTIONS = '-o StrictHostKeyChecking=no'
        REMOTE_USER = 'ubuntu'
        REMOTE_HOST = '172.31.9.161'
    }
    stages {
        stage('Git Clone') {
            steps {
                git url: 'https://github.com/sushant960kr/php-project.git', branch: 'master'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                    sh 'docker images'
                }
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh '''
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        if [ $? -ne 0 ]; then
                            echo "Docker login failed"
                            exit 1
                        fi
                    '''
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${DOCKER_IMAGE}"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def dockerrm = "sudo docker rm -f ${CONTAINER_NAME} || true"
                    def dockerCmd = "sudo docker run -itd --name ${CONTAINER_NAME} -p 8083:80 ${DOCKER_IMAGE}"

                    sshagent(['sshkeypair']) {
                        // Execute Docker login and commands on the remote server
                        sh """
                            ssh ${SSH_OPTIONS} ${REMOTE_USER}@${REMOTE_HOST} '
                                echo "$PASS" | docker login -u "$USER" --password-stdin && \
                                ${dockerrm} && \
                                ${dockerCmd}
                            '
                        """
                    }
                }
            }
        }
    }
}
