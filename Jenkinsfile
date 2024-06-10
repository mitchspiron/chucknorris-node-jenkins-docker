pipeline {
    agent any
    stages {
        stage ("checkout") {
            steps {
                checkout scm
            }
        }
        stage ("Build") {
            steps {
                bat 'npm install'
                bat 'npm run build'
            }
        }
        stage ("Build image") {
            steps {
                bat 'docker build . -t chucknorris'
            }
        }
        stage ("Push image") {
            steps {
                bat 'echo %DOCKERHUB_USERNAME%'
                withCredentials([usernamePassword(credentialsId: 'docker_cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    bat 'docker login -u %DOCKERHUB_USERNAME% -p %DOCKERHUB_PASSWORD%'
                    bat 'docker tag chucknorris mitchspiron/chucknorris'
                    bat 'docker push mitchspiron/chucknorris'
                    bat 'docker logout'
                }
            }
        }
    }
}