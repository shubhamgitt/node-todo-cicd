pipeline {
    agent any
    stages {
        stage("code"){
            steps{
                git url: "https://github.com/shubhamgitt/node-todo-cicd.git", branch: "master"
            }
        }
        stage("build test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("push to repository"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-app-test-new ${env.dockerHubUser}/node-app-test-new:latest"
                    sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
