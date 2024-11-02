@Library("shared") _
pipeline{
    agent {label "nagu"}
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
            
        }
        stage("code"){
            steps{
                echo "this is cloning the code"
                git url: "https://github.com/hattymatty1/django-notes-app.git", branch: "main"
                echo "Code Cloning Successful"
            }
        }
        stage("build"){
            steps{
                echo "this is building the code"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("Pushing to the DockerHub"){
            steps{
                echo "this is pushing to the dockerHub"
                withCredentials([usernamePassword(credentialsId:"DockerHubCred", usernameVariable:"dockerHubUser", passwordVariable:"dockerHubPass")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                echo "this is deploying the code"
                sh "docker compose up -d"
            }
        }
        
    }
}
