pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/adeelfarooq01/devops-jenkins-ec2.git'
            }
        }

        stage('SSH Test') {
            steps {
                sh 'ssh -o ConnectTimeout=10 -i "/home/jenkins/keys/sp22-bse-030_key.pem" sp22-030@20.198.20.235 whoami'
            }
        }

        stage('Deploy HTML Page') {
            steps {
                sh 'scp -i "/home/jenkins/keys/sp22-bse-030_key.pem" index.html sp22-030@20.198.20.235:/home/sp22-030/devops-app/'
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
