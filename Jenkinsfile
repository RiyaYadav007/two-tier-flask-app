@Library("Shared") _
pipeline{
    
    agent { label "dev"};
    
    stages{
        stage("Code Clone"){
            steps{
               script{
                   clone("https://github.com/RiyaYadav007/two-tier-flask-app.git", "master")
               }
            }
        }
    } 
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
            
        }
        stage("Test"){
            steps{
                echo "Developer / Tester tests likh ke dega..."
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                script{
                    docker_push("dockerhubcreds","two-tier-flask-app")
                }  
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    


    
}
