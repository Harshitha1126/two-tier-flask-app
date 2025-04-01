pipeline {
    agent { label "dev"};
    
    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Harshitha1126/two-tier-flask-app.git", branch: "Feature_modified"
                echo "code completed"
            }
        }
        stage("test") {
            steps {
                echo "testing completed"
            }
        }
        stage("build") {
            steps {
                sh "docker build -t two-tier-flask-app ."
                echo "build completed"
            }
        }
        stage("docker push") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerhub_creds", 
                    usernameVariable: "dockerhubuser",
                    passwordVariable: "dockerhubpassword"
                )]) {
                    sh "docker login -u ${dockerhubuser} -p ${dockerhubpassword}"
                    sh "docker image tag two-tier-flask-app ${dockerhubuser}/two-tier-flask-app"
                    sh "docker push ${dockerhubuser}/two-tier-flask-app:latest"
                    echo "application has been deployed"
                }
            }
        }
        stage("deploy") {
            steps {
                sh "docker compose up -d --build flask-app"
                echo "build completed"
            }
        }
    }
}
