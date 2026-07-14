pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Hello') {
            steps {
                echo 'Pipeline is working!'
            }
        }
        stage('Terraform Version') {
            steps {
                sh 'terraform --version'
            }
        }
        stage('Terraform Format') {
            steps {
                sh 'terraform fmt -check -recursive'
            }
        }
                stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
    }
}