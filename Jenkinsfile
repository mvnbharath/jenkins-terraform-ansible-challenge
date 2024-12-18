pipeline {
    agent any

    stages {
        

        stage('Checkout') {
            steps {
                deleteDir()
                sh 'echo cloning repo'
                sh 'git clone https://github.com/mvnbharath/jenkins-terraform-ansible-challenge.git' 
            }
        }
        
        stage('Terraform Apply') {
            steps {
                script {
                    dir('/var/lib/jenkins/workspace/challenge6/jenkins-terraform-ansible-challenge/') {
                    sh 'pwd'
                    sh 'terraform init'
                    
                    sh 'terraform plan'
                    sh 'terraform apply -auto-approve'
                    }
                }
            }
        }
        
        stage('Ansible Deployment') {
            steps {
                script {
                   sleep '360'
                    ansiblePlaybook becomeUser: 'ec2-user', credentialsId: 'aws', disableHostKeyChecking: true, installation: 'ansible', inventory: '/var/lib/jenkins/workspace/challenge6/jenkins-terraform-ansible-challenge/inventory.yaml', playbook: '/var/lib/jenkins/workspace/challenge6/jenkins-terraform-ansible-challenge/amazon-playbook.yml', vaultTmpPath: ''
                    ansiblePlaybook become: true, credentialsId: 'aws', disableHostKeyChecking: true, installation: 'ansible', inventory: '/var/lib/jenkins/workspace/challenge6/jenkins-terraform-ansible-challenge/inventory.yaml', playbook: '/var/lib/jenkins/workspace/challenge6/jenkins-terraform-ansible-challenge/ubuntu-playbook.yml', vaultTmpPath: ''
                }
            }
        }
    }
}
