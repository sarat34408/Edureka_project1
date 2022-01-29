pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git branch: 'main', url: 'https://github.com/sarat34408/edureka_project1.git'
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build . -t sarat34408/sarat34408/my-php-website"
            }
        }
        stage('DockerHub Push'){
            steps{
                
                withCredentials([string(credentialsId: 'sarat34408', variable: 'dockerPwd')]) {
                      sh "docker login -u sarat34408 -p ${dockerPwd}"
                }
                
                sh "docker push sarat34408/sarat34408/my-php-website "
            }
        }
        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

