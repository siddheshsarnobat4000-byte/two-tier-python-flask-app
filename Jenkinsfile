pipeline {
    
    agent any;
    
    stages {
        stage("code"){
            steps{
               git url: "https://github.com/siddheshsarnobat4000-byte/two-tier-python-flask-app.git", branch: "master"
            }
        }
        stage("build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("test"){
            steps{
             echo "Devloper / Tester test likh ke dega"   
            }
        }
        stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerhubcreds", 
                    passwordVariable: "dockerhubpass",
                    usernameVariable: "dockerhubuser"
                    )]){
                    
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass} "
                sh "docker image tag two-tier-flask-app ${env.dockerhubuser}/two-tier-flask-app"
                sh "docker push ${env.dockerhubuser}/two-tier-flask-app:latest"
                
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d --build flaskapp"
            }
        }
   }
        
}
