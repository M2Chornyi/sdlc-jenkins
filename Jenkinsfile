test_cals = ["Victory+or+Death","Lol","Okay","Hey","I+obey","By+my+Axe","Well+Met" ]

pipeline {
    agent any
    parameters {
        choice( name: 'STACK',    choices: ['blue','green'], description: 'Select environment stack')
        text(   name: "VERSION",  defaultValue: "0.0.1")
        text(   name: "NAMESPACE",defaultValue: "default")
    }
    stages {
        stage('Build docker image'){
            steps{
                sh """eval $(minikube -p minikube docker-env) && docker build -t th3-python:${params.VERSION} """
            }
        }
        stage('Verification'){
            steps{
                sh """if kubectl -n ${params.NAMESPACE} get svc application ; then echo [INFO]: Service exist! ; else echo [INFO]: Creating service... &&  kubectl create -n ${params.NAMESPACE} service loadbalancer application --tcp=8080:8080 --dry-run=client -o yaml | kubectl -n ${params.NAMESPACE} apply -f - ; fi"""
            }
        }
        stage('HELM install') {
            steps {
                sh "helm -n ${params.NAMESPACE} upgrade -i ${params.STACK} development-lyfecycle/th3-server --set image.tag=${params.VERSION} --set stack=${params.STACK}"
            }
        }
        stage('Test version') {
            steps {
                sh "kubectl -n ${params.NAMESPACE} run testbox-${params.STACK} --image=nginx --restart=Never --rm -it -- curl ${params.STACK}-th3-server:8080/version"
            }
        }
        stage('Test vocabuary') {
            steps {
                script {
                   test_cals.each { item ->
                       stage ("Testing $item") {
                             sh "kubectl -n ${params.NAMESPACE} run testbox-${params.STACK} --image=nginx --restart=Never --rm -it -- curl ${params.STACK}-th3-server:8080/api/v1/translate?phrase=${item}"
                       }
                   }
               }
            }
        }
        stage('Ready to flip?') {
            steps {
                input 'Would you like to make it LIVE?'
            }
        }
        stage('Deploy') {
            steps {
                sh """kubectl -n ${params.NAMESPACE} patch service application --type='json' -p='[{"op": "replace", "path": "/spec/selector", "value":{ "stack": "${params.STACK}" } }]'"""
                sh "kubectl -n ${params.NAMESPACE} run testbox-${params.STACK} --image=nginx --restart=Never --rm -it -- curl application:8080/version"
            }
        }
    }
}