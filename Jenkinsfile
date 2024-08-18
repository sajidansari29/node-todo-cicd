pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/sajidansari29/node-todo-cicd.git”, branch:”master”
            }
            
        }
        
        stage("Build"){
            steps{
                echo "building the code"
                sh " docker build . -t todo-node-app"
                
            }
            
        }
        stage("Push to Docker"){
            steps{
                echo "Pushing the code to docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker tag my-todo-app ${env.dockerHubUser}/my-todo-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-todo-app:latest”
                
                }
            }
            
        }
        stage("Deploy"){
            steps{
                echo "Deploying the code"
                sh “docker compose down && docker compose up -d"
                
            }
        }
        
    }
}
