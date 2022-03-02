pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mukund2618/capstone2.git']]])
            }
        }
        stage('Terraform init') {
            steps {
                sh ("terraform init");
            }
        }
        stage('Terraform action') {
            steps {
                echo "terraform parameter action is --> ${TF-Action}"
                sh ("terraform ${TF-Action} --auto-approve");
            }
        }
    }
}
