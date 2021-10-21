pipeline {
    agent any
    parameters {
        choice( name: 'STACK',    choices: ['blue','green'], description: 'Select environment stack')
        text(   name: "VERSION",  defaultValue: "0.0.1")
        text(   name: "NAMESPACE",defaultValue: ["default"])
    }
    stages {
        stage('Verification'){
            sh """if kubectl -n ${params.NAMESPACE} get svc application ; then echo [INFO]: Service exist! ; else echo [INFO]: Creating service... &&  kubectl create -n ${params.NAMESPACE} service loadbalancer application --tcp=80:8080 --dry-run=client -o yaml | kubectl -n ${params.NAMESPACE} apply -f - ; fi"""
        }
        stage('HELM install') {
            steps {
                sh "helm -n ${params.NAMESPACE} upgrade -i ${params.STACK} development-lyfecycle/th3-server --set image.tag=${params.VERSION} --set stack=${params.STACK}"
            }
        }
        stage('Test') {
            steps {
                sh """
                kubectl -n ${params.NAMESPACE} run testbox-${params.STACK} --image=nginx --restart=Never --rm -it -- curl ${params.STACK}-th3-server:8080/version ;
                for i in "Victory+or+Death" "Lol" "Okay" "Hey" "I+obey" "By+my+Axe" "Well+Met" ; \
                do kubectl -n ${params.NAMESPACE} run testbox-${params.STACK} --image=nginx --restart=Never --rm -it -- curl ${params.STACK}-th3-server:8080/api/v1/translate?phrase=$i; done
                """
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}