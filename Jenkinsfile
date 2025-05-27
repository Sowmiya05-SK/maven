pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9' // Make sure this matches the Maven name in Jenkins Global Tool Configuration
        jdk 'JDK 21'        // Change to 'JDK_11' or other if you're using a different version
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building the project...'
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                bat 'mvn test'
            }

            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                bat 'mvn package'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check logs for errors.'
        }
    }
}
