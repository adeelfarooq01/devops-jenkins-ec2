pipeline {
    agent any

    environment {
        // Ensure this matches your SSH Private Key ID in Jenkins
        SSH_CRED_ID = 'github-token' 
        REMOTE_USER = 'sp22-030'
        REMOTE_HOST = '20.198.20.235'
        // Pointing directly to the Nginx default root
        LIVE_DIR    = '/var/www/html'
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Validate HTML Files') {
            steps {
                sh 'ls -l index.html'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Static site: No compilation needed."'
            }
        }

        stage('Deploy Application') {
            steps {
                sshagent([SSH_CRED_ID]) {
                    sh '''
                    # 1. Clear old files from the live directory
                    ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} "rm -rf ${LIVE_DIR}/*"
                    
                    # 2. Copy the new index.html and files to the live directory
                    scp -r * ${REMOTE_USER}@${REMOTE_HOST}:${LIVE_DIR}/
                    
                    echo "Deployment to http://${REMOTE_HOST} is complete!"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Changes are now live on the server.'
        }
        failure {
            echo 'FAILURE: Deployment failed. Check Jenkins credentials and VM permissions.'
        }
    }
}
