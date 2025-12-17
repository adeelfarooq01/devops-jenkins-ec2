pipeline {
    agent any

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
                echo "HTML project ready"
                '''
            }
        }
    }
}
