pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main',
                url: 'https://github.com/sarthak-agnihotri/node-webhook-demo.git'
            }
        }
        stage('Install Dependencies'){
            steps{
                bat 'npm install'
            }
        }
        stage('Build Docker Image'){
            steps{
                bat 'docker build -t sarthak0144/node-webhook-demo:latest .'
            }
        }
        stage('Push Docker Image'){
            steps{
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]){
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push sarthak0144/node-webhook-demo:latest'
                }
            }
        }
    }
    post {

        success {

            echo 'Pipeline Successful'

        }

        failure {

            echo 'Pipeline Failed'

        }

    }

}