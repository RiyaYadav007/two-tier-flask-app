@Library("Shared") _

pipeline {
    agent { label "dev" }

    stages {
        stage("Code Clone") {
            steps {
                script {
                    // Make sure your Shared library has a clone function
                    clone("https://github.com/RiyaYadav007/two-tier-flask-app.git", "master")
                }
            }
        }
        
        stage("Build") {
            steps {
                sh "docker build -t two-tier-flask-app ."
            }
        }
        
        stage("Test") {
            steps {
                echo "Developer / Tester tests will be added here..."
            }
        }
        
        stage("Push to Docker Hub") {
            steps {
                script {
                    // Make sure your Shared library has a docker_push function
                    docker_push("dockerhubcreds", "two-tier-flask-app")
                }
            }
        }
        
        stage("Deploy") {
            steps {
                sh "docker compose up -d --build flask-app"
            }
        }
    }

    post {
        success {
            script {
                emailext(
                    from: 'akpatel851900@gmail.com',
                    to: 'akpatel851900@gmail.com',
                    subject: 'Jenkins Build Successful',
                    body: 'Build was successful. Check your application!'
                )
            }
        }
        
        failure {
            script {
                emailext(
                    from: 'akpatel851900@gmail.com',
                    to: 'akpatel851900@gmail.com',
                    subject: 'Jenkins Build Failed',
                    body: 'Build failed. Please check the logs for more details.'
                )
            }
        }
    }
}
