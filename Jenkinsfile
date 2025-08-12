pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                buildApp()
            }
        }

        stage('Test') {
            steps {
                runTests()
            }
        }

        stage('Deploy') {
            steps {
                deployApp()
            }
        }
    }

    post {
        always {
            cleanupWorkspace()
        }
    }
}