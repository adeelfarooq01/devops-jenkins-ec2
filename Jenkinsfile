pipeline {
    agent any

    environment {
        SSH_KEY = '/home/jenkins/keys/sp22-bse-030_key.pem'
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

        // REMOVED the extra "stages {" line that was here
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
    } // End of the single stages block

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
