pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                shell('kubectl get all')
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