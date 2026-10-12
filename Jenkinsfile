
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code retrieved from GitHub'
            }
        }

        stage('Check Java') {
            steps {
                sh 'java -version'
            }
        }

        stage('Check Project Files') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                echo 'Build stage started successfully'
                echo 'Configure your project build command here'
            }
        }

        stage('Complete') {
            steps {
                echo 'Jenkins pipeline completed successfully!'
            }
        }
    }
}
