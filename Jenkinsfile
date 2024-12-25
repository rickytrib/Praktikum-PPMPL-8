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
            post {
                success {
                emailext subject: 'Checkout Succeeded', body: 'The Checkout succeeded!', 
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
                failure {
                    emailext subject: 'Checkout Failed', body: 'The Checkout failed.', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
            post {
                success {
                    emailext subject: 'Install Dependencies Succeeded', body: 'The Install Dependencies succeeded!', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
                failure {
                    emailext subject: 'Install Dependencies Failed', body: 'The Install Dependencies failed.', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
            }
            
        }
        stage('Run Unit Tests') {
            steps {
                bat 'npm test:unit'
            }
            post {
                success {
                    emailext subject: 'test Succeeded', body: 'The test succeeded!', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
                failure {
                    emailext subject: 'test Failed', body: 'The test failed.', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Tambahkan perintah build jika diperlukan
                bat 'npm run build'
            }
            post {
                success {
                emailext subject: 'Build Succeeded', body: 'The Build succeeded!', 
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
                failure {
                    emailext subject: 'Build Failed', body: 'The Build failed.', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy the application...'
            }
            post {
                success {
                emailext subject: 'Deploy Succeeded', body: 'The Deploy succeeded!', 
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
                failure {
                    emailext subject: 'Deploy Failed', body: 'The Deploy failed.', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
            }
            
        }

        stage('Integration tests') {
            steps {
                echo 'Running integration tests...'
                // Tambahkan perintah untuk menjalankan integration 
                bat 'npm run tests:integration'
            }
            post {
                success {
                emailext subject: 'Integration tests Succeeded', body: 'The Integration test succeeded!', 
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
                failure {
                    emailext subject: 'Integration tests Failed', body: 'The Integration tests failed.', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }   
            }    
        }
    }
    
    post {
        success {
            echo 'Pipeline finished successfully!'
            emailext subject: 'Pipeline Succeeded', body: 'The Pipeline succeeded!', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }
        failure {
            echo 'Pipeline failed!'
            emailext subject: 'Pipeline Failed', body: 'The Pipeline failed.', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }
    }
}
