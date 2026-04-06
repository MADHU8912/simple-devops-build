pipeline {
    agent any

    triggers {
        cron('H/5 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking source code'
            }
        }

        stage('Check Files') {
            steps {
                bat 'dir'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t simple-devops-app .'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat 'docker rm -f simple-devops-container || exit /b 0'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run --name simple-devops-container simple-devops-app'
            }
        }

        stage('Save Build Log') {
            steps {
                bat 'echo Build completed successfully > build-log.txt'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'build-log.txt', fingerprint: true
        }
    }
}