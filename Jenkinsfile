pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mikesobukonla/terraform-test-ms.git'
            }
        }

        stage('Initialize Terraform') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Plan Terraform') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Apply Terraform') {
            steps {
                input message: "Approve deployment?", ok: "Deploy"
                sh 'terraform apply tfplan'
            }
        }

        stage('Destroy Terraform') {
            steps {
                input message: "Approve destruction?", ok: "Destroy"
                sh 'terraform destroy -auto-approve'
            }
        }
    }
}
