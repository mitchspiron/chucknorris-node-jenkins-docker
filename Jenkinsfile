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
                withCredentials([usernamePassword( credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    def registry_url = "registry.hub.docker.com/"
                    bat 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD ${registry_url}'
                    docker.withRegistry("http://${registry_url}", "docker-hub-credentials") {
                        bat 'docker tag chucknorris mitchspiron/chucknorris'
                        bat 'docker push mitchspiron/chucknorris'
                    }
                    bat 'docker logout'
                }
            }
        }
    }
}