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
post {
    success {
        emailtext(
        subject: "Build Successful",
            body: "Good News: Your build was successfull!",
            to: 'akpatel851900@gmail.com'
        )
    }
    failure {
        emailtext(
        subject: "Build Failed",
            body: "Bad News: Your build was Failed!",
            to: 'akpatel851900@gmail.com'
        )
    }
}    


    
}
