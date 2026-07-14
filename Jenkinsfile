pipeline {
    agent any

        options {
        skipDefaultCheckout(true)
         timestamps()
    }
    environment {
        AWS_REGION = 'us-east-1'
    }

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
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-creds',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ])
                sh 'terraform fmt -check -recursive'
            }
        }
                stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }
                stage('Terraform plan') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-creds',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ])
            terraform plan -out=tfplan            }
        }
    }
}