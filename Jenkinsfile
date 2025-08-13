pipeline {
    agent any

    environment {
        AUTHOR = "Ghulam Muzaki"
        EMAIL = "echo.ghulammuzaki1201@gmail.com"
    }
    triggers {
        pollSCM("*/5 * * * *")
    }

    stages {
        stage('Prepare') {
            agent {
                label "ubuntu" // Penulisan yang lebih ringkas
            }
            steps {
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }

        stage('Build') {
            steps {
                echo "🔨 Build aplikasi..."
                // Ganti dengan perintah build yang sesungguhnya, contoh:
                // sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Menjalankan test..."
                // Ganti dengan perintah test yang sesungguhnya, contoh:
                // sh 'mvn test'
                // junit 'target/surefire-reports/*.xml'
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploy aplikasi..."
                // Ganti dengan perintah deploy yang sesungguhnya, contoh:
                // sh './deploy-to-server.sh'
            }
        }
    }

    post {
        // Notifikasi akan dikirim jika pipeline berhasil
        success {
            slackSend(color: '#2eb886', message: "✅ Berhasil: Job '${env.JOB_NAME}' (build ${env.BUILD_NUMBER}) berhasil selesai.")
        }
        // Notifikasi akan dikirim jika pipeline gagal
        failure {
            slackSend(color: '#a30200', message: "❌ Gagal: Job '${env.JOB_NAME}' (build ${env.BUILD_NUMBER}) gagal! Lihat di ${env.BUILD_URL}")
        }
    }
}