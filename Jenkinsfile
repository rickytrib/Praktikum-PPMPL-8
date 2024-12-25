pipeline {
    agent any
    
    environment {
        CI = 'true'
        STAGING_SERVER = 'staging.example.com' // Ganti dengan alamat server staging Anda
        STAGING_USER = 'user' // Ganti dengan username server staging Anda
        SSH_CREDENTIALS_ID = 'ssh-staging-credentials' // ID kredensial SSH di Jenkins
        PPUTTY_PATH = 'C:\\path\\to\\putty' // Path ke direktori PuTTY (pscp dan plink)
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rickytrib/Praktikum-PPMPL-8.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Unit Tests') {
            steps {
                bat 'npm test'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Tambahkan perintah build jika diperlukan
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to Staging Server...'
                // Tambahkan perintah deploy jika diperlukan
                withCredentials([sshUserPrivateKey(credentialsId: env.SSH_CREDENTIALS_ID, keyFileVariable: 'SSH_KEY_PATH')]) {
                        bat """
                        ${PPUTTY_PATH}\\pscp -i "%SSH_KEY_PATH%" -r build\\ ${STAGING_USER}@${STAGING_SERVER}:/path/to/deploy/
                        ${PPUTTY_PATH}\\plink -i "%SSH_KEY_PATH%" ${STAGING_USER}@${STAGING_SERVER} "cd /path/to/deploy && ./restart-staging.sh"
                        """
                }
            }
        }
        stage('Integration tests')
            steps {
                echo 'Running integration tests...'
                // Tambahkan perintah untuk menjalankan integration tests
            }
    }
    
    post {
        success {
            echo 'Pipeline finished successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }

    post {
        success {
            emailext subject: 'Build Succeeded', body: 'The build succeeded!', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }
        failure {
            emailext subject: 'Build Failed', body: 'The build failed.', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }
    }
}
