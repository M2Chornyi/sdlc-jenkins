pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                shell ('kubeclt --version')
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}