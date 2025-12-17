pipeline {
    agent any

    environment {
        // This is your SSH credential ID in Jenkins (Manage Jenkins -> Credentials)
        // Make sure the ID in Jenkins is EXACTLY 'deploy-ssh-key'
        SSH_CRED_ID = 'github-token' 
        REMOTE_USER = 'sp22-030'
        REMOTE_HOST = '20.198.20.235'
        REMOTE_DIR  = '~/html'
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
                sh 'echo "No build required for static HTML project"'
            }
        }

        stage('Deploy Application') {
            steps {
                // We use the ID defined in the environment block
                sshagent([SSH_CRED_ID]) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} "mkdir -p ${REMOTE_DIR}"
                    scp -r * ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}/
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
