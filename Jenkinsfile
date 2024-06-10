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
    }
}