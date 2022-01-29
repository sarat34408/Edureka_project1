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
                sh "docker build . -t saratdevops/edureka/my-php-website"
            }
        }
        stage('DockerHub Push'){
            steps{
                
                withCredentials([string(credentialsId: 'docker_devops', variable: 'dockerPwd')]) {
                      sh "docker login -u sarat34408 -p ${dockerPwd}"
                }
                
                sh "docker push saratdevops/edureka/my-php-website"
            }
        }
        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'test-server',disableHostKeyChecking:true, installation: 'ansible', inventory: 'servers.inv', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', disableHostKeyChecking:true,installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

