pipeline {
    agent any

    tools {
        jdk 'JDK-17'
        maven 'Maven-3.9'
    }

    options {
        disableConcurrentBuilds()
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        stage('2. Build') {
            steps {
                echo 'Compiling Java source'
                sh 'mvn clean compile'
            }
        }

        stage('3. Unit Test') {
            steps {
                echo 'Running unit tests'
                sh 'mvn test'
            }
            post {
                always {
                    junit allowEmptyResults: false,
                          testResults: '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('4. Package') {
            steps {
                echo 'Creating the JAR'
                sh 'mvn package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }

        stage('5. Deploy') {
            steps {
                echo 'Copying the application artifact'
                sh '''
                    set -eu
                    mkdir -p "$WORKSPACE/deployment"
                    cp target/my-java-app-1.0.0.jar \
                       "$WORKSPACE/deployment/deployed-app.jar"
                    ls -lh "$WORKSPACE/deployment/deployed-app.jar"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
