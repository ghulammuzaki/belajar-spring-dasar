pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "🔨 Build aplikasi..."
            }
        }
        stage("pereppare") {
            agent {
                node {
                  label "ubuntu"
                }
            }
            steps {
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Menjalankan test..."
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploy aplikasi..."
            }
        }
    }
}
