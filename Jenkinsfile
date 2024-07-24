pipeline {
    agent {
        label 'AGENT-1'
    }

     options {
            
            timeout(time: 30, unit: 'MINUTES')
            disableConcurrentBuilds()
            ansiColor('xterm')
    }
    parameters{
        string(name: 'appVersion', defaultValue: '1.0.0', description: 'what is the application Version?')
    }
    environment{
        def appVersion = '' // variable declaration
        nexusUrl = 'nexus.shivdev.online:8081'
    }
    stages {
        stage('Print the app version'){
            steps{
                script{
                   echo "Application version: ${params.appVersion}"
                }
            }
        }
        stage('init'){
            steps{
                sh """
                    cd terraform
                    terraform init -reconfigure
                """
            }
        }
        stage('plan'){
            steps{
                sh """
                    pwd
                    cd terraform 
                    terraform plan -var="app_version=${params.appVersion}"
                """
            }
        }
        stage('deploy'){
            steps{
                sh """
                    pwd
                    cd terraform
                    terraform apply -auto-approve -var="app_version=${params.appVersion}"
                """
            }
        }
    }

    post { 
        
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success { 
            echo 'I will run when pipeline is success'
        }
        failure { 
            echo 'I will run when pipeline is failure'
        }
    }
}


