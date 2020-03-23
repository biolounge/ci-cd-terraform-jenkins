## Jenkins pipleine script for terraform
`
pipeline {
      agent any

      stages {
           stage('checkout') {
            steps {
               git 'https://github.com/biolounge/ci-cd-terraform-jenkins.git'
            }
         }
         
           stage('Set Terraform') {
            steps {
                    sh "cd /tmp"
                    sh "curl -o terraform.zip https://releases.hashicorp.com/terraform/0.12.24/terraform_0.12.24_linux_amd64.zip"
                    sh "rm -rf terraform"
                    sh "unzip terraform.zip"
                    sh "chmod +x terraform"
                    sh "pwd"
            }
         }
 
           stage('Provision infrastructure') {
            steps {
                sh './terraform init'
                sh './terraform plan -out=plan'
                sh './terraform apply plan'
            }
           }

    }
}
`
