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
    }
}