pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/sushant960kr/php-project.git/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sushant960kr/sushantnewimage:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                 withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    // Using triple single quotes to prevent Groovy string interpolation for better security
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
        
     stage('Deploy') {
            steps {
               script {
                    // Commands to remove existing container and run the new one
                    def dockerrm = "sudo docker rm -f ${CONTAINER_NAME} || true"
                    def dockerCmd = "sudo docker run -itd --name ${CONTAINER_NAME} -p 8083:80 ${DOCKER_IMAGE}"

                    sshagent(['sshkeypair']) {
                        // Executing SSH commands to manage Docker containers on the remote server
                        sh "ssh ${SSH_OPTIONS} ${REMOTE_USER}@${REMOTE_HOST} '${dockerrm}'"
                        sh "ssh ${SSH_OPTIONS} ${REMOTE_USER}@${REMOTE_HOST} '${dockerCmd}'"
                    
                    }
                }
            }
        }
    }
}
