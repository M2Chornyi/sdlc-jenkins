pipeline {
    agent any
    parameters {
        choice(name: 'STACK', choices: "choice", description: 'Select environment stack')
    }
    scm('')
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