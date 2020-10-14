pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "sudo docker build . -t ayiangio/react-zalora-kw:${DOCKER_TAG} ."
            }
        }
        stage('Push Docker Hub'){
            steps{
                withCredentials([string(credentialsId: 'pwd_hub', variable: 'pwd_hub')]) {
                    sh "sudo docker login -u ayiangio -p ${pwd_hub}"
                    sh "sudo docker push ayiangio/react-zalora-kw:${DOCKER_TAG}"
                }
            }
        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}