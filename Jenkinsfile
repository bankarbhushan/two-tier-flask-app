pipeline {
    agent any
    stages {
        stage("Code") {
            steps {
                git url:"https://github.com/bankarbhushan/two-tier-flask-app.git", branch:"master"
            }
        }
        stage("Build") {
            steps {
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("Test") {
            steps {
                echo "developer bhai ne test diya..."
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHubCreds", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]) {
                    sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                    sh "docker image tag two-tier-flask-app ${dockerHubUser}/two-tier-flask-app"
                    sh "docker push ${dockerHubUser}/two-tier-flask-app:latest"
                }
        }
    }
        stage("Deploy") {
            steps {
               sh "docker compose up -d --build flask-app"
            }
        }
    }
}
