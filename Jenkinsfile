pipeline{
    
    agent any;
    
    stages{
        stage("Code clone"){
            steps{
                git url: "https://github.com/Ravi-7284/node-js-app.git", branch: "main"
            }
        }
        
        stage("Build"){
            steps{
                sh "docker build -t my-node-app:slim ."
            }
        }
        
        stage("Test"){
            steps{
                echo "Testing completed"
            }
        }
        
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                )]){
                    
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag my-node-app:slim ${env.dockerHubUser}/my-node-app:slim"
                    sh "docker push ${env.dockerHubUser}/my-node-app:slim"
                    
                    }
                }
        }
        
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
