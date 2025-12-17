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

        stage('Deploy Application') {
            steps {
                sh '''
                echo "Deploying HTML project to Azure VM..."
                # Create the remote directory if it doesn't exist
                ssh -o StrictHostKeyChecking=no -i $SSH_KEY $REMOTE_USER@$REMOTE_HOST "mkdir -p $REMOTE_DIR"
                
                # Copy all files from Jenkins workspace to the VM
                scp -i $SSH_KEY -r * $REMOTE_USER@$REMOTE_HOST:$REMOTE_DIR/
                
                # Optionally list files on VM to verify
                ssh -i $SSH_KEY $REMOTE_USER@$REMOTE_HOST "ls -l $REMOTE_DIR"
                '''
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
