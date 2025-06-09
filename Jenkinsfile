pipeline {
    agent any // You can specify a specific agent label if needed, e.g., agent { label 'terraform-agent' }


    stages {
        stage('Checkout Code') {
            steps {
                // Using your specified Git URL and credential ID
                git branch: 'main', credentialsId: 'github-tocken', url: 'https://github.com/Shirisha95-palla/terraform-hub.git'
                // IMPORTANT: Ensure 'main' is the correct branch name. Change to 'master' if needed.
                // The 'github-manikiran7-pat' credential must be configured in Jenkins Credentials.
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                script {
                    sh 'terraform plan -out=tfplan'
                }
            }
        }

        stage('Terraform Apply (Manual Approval)') {
            steps {
                input message: 'Proceed with Terraform Apply for local_file?', ok: 'Apply'
                script {
                    sh 'terraform apply -auto-approve tfplan'
                }
            }
        }

        // Optional: Stage to destroy the resource
        stage('Terraform Destroy (Manual Approval)') {
            steps {
                input message: 'DO YOU REALLY WANT TO DESTROY THE LOCAL FILE?', ok: 'Destroy'
                script {
                    sh 'terraform destroy -auto-approve'
                }
            }
        }
    }
}