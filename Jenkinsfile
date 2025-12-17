pipeline {
    agent any

    environment {
        VM_USER = "sp22-030"                          // VM username
        VM_IP   = "20.198.20.235"                     // VM public IP
        SSH_KEY = "/home/jenkins/keys/sp22-bse-030_key.pem" // Path to SSH private key on Jenkins
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
                ssh -o StrictHostKeyChecking=no -i ${SSH_KEY} ${VM_USER}@${VM_IP} << EOF
                mkdir -p ~/devops-app
                cp -r * ~/devops-app/
                echo "Files deployed successfully!"
                EOF
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Completed Successfully!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
