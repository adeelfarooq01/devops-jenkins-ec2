pipeline {
    agent any

    environment {
        // Path to your SSH private key on Jenkins server
        SSH_KEY = '/home/jenkins/keys/sp22-bse-030_key.pem'
        // Remote server details
        REMOTE_USER = 'sp22-030'
        REMOTE_HOST = '20.198.20.235'
        REMOTE_DIR = '~/html'
    }

    stages {

        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Validate HTML Files') {
            steps {
                sh '''
                echo "Checking HTML files..."
                ls *.html
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                echo "No build required for static HTML project"
                '''
            }
        }

        stages {
        stage('Deploy Application') {
            steps {
                sshagent(['github-token']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no sp22-030@20.198.20.235 "mkdir -p ~/html"
                    scp -r * sp22-030@20.198.20.235:~/html/
                    '''
                }
            }
        }
    }
    

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
}
