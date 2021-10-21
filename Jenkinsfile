pipeline {
    agent any
    parameters {
        choice(name: 'STACK', choices: ['blue','green'], description: 'Select environment stack')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building.. ${params.STACK}'
                sh 'kubectl get all'
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