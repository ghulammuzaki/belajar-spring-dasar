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
                label "ubuntu"
            }
            steps {
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }

        stage('Build & Test in Parallel') {
            parallel {
                stage('Build') {
                    steps {
                        echo "🔨 Build aplikasi..."
                        // sh 'mvn clean install'
                    }
                }

                stage('Test') {
                    steps {
                        echo "🧪 Menjalankan test..."
                        // sh 'mvn test'
                        // junit 'target/surefire-reports/*.xml'
                    }
                }
            }
        }

        stage('Deploy') {
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "ghlmmz"
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'deploy-credentials', 
                                                  usernameVariable: 'DEPLOY_USER', 
                                                  passwordVariable: 'DEPLOY_PASS')]) {
                    sh '''
                        echo "🚀 Deploy aplikasi..."
                        echo "Login dengan user: $DEPLOY_USER"
                        # Jangan echo password di log!
                        
                        # Contoh pakai username & password untuk login:
                        # curl -u $DEPLOY_USER:$DEPLOY_PASS https://server-deploy/api/deploy
                    '''
                }
            }
        }
    }

    post {
        success {
            slackSend(color: '#2eb886', message: "✅ Berhasil: Job '${env.JOB_NAME}' (build ${env.BUILD_NUMBER}) berhasil selesai.")
        }
        failure {
            slackSend(color: '#a30200', message: "❌ Gagal: Job '${env.JOB_NAME}' (build ${env.BUILD_NUMBER}) gagal! Lihat di ${env.BUILD_URL}")
        }
    }
}
