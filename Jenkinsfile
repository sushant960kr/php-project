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
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 sushant960kr/sushantnewimgage:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.9.161 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.9.161 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
