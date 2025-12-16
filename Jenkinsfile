pipeline {
    agent any

    stages {

        stage('Checkout Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/adeelfarooq01/devops-jenkins-ec2.git'
            }
        }

        stage('SSH Test') {
            steps {
                sshagent(['github-token']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no \
                        -o ConnectTimeout=10 \
                        sp22-030@20.198.20.235 whoami
                    '''
                }
            }
        }

        stage('Deploy HTML Page') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                        scp -o StrictHostKeyChecking=no \
                        index.html \
                        sp22-030@20.198.20.235:/home/sp22-030/devops-app/
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment Completed Successfully!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}