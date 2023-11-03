pipeline{
    
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "Code clone ho gya hai"
                git url: 'https://github.com/dshri12/node-todo-cicd.git', branch: "master"
            }
        }
        stage("Code Build & Test"){
            steps{
                echo "code toh build bhi kar diya gaya hai"
                sh "docker build -t node-app-demo ."
            }
        }
        stage("Push to Repository"){
            steps{
                echo "ab main bani hui image ko docker hub me push karduga"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker tag node-app-demo ${env.dockerhubUser}/node-app-demo:latest"
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker push ${env.dockerhubUser}/node-app-demo:latest"
                }
            }
        }
        stage("Deployed The Code"){
            steps{
                echo "And finally we have deployed the code aur hum jeet gaye!"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
