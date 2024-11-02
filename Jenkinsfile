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
                script{
                    clone("https://github.com/hattymatty1/django-notes-app.git", "main")
                }
            }
        }
        stage("build"){
            steps{
                script{
                    docker_build("notes-app", "latest", "souravk45")
                }
                
            }
        }
        stage("Pushing to the DockerHub"){
            steps{
                script{
                    docker_push("notes-app","latest")
                }
            }
        }
        stage("deploy"){
            steps{
                script{
                    deploy()                    
                }
            }
        }
        
    }
}
