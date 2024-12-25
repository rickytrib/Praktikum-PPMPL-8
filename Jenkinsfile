pipeline {
    agent any
    
    environment {
        CI = 'true'
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
                echo 'Deploy the application...'
                input 'Do you approve deployment?'
                node {
                    //deploy things
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
