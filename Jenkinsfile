pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = "us-east-2"
        GIT_BR = "main"
    }
    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev', 'prod', 'main'], description: 'Select the environment to deploy application')
    }
    stages {
        stage('checkout') {
            
            /*steps {
                git branch: "${params.ENVIRONMENT}", changelog: false, poll: false, url: 'https://github.com/Umarali-99/Otel-python-sample.git'
            }*/
        }
        
        stage('Read Properties') {
            steps {
                script {
                    def props = readJSON file: 'frontend-properties.json'
                    def envProps = props[params.ENVIRONMENT]
                    if (envProps == null) {
                        error "No properties found for environment: ${params.ENVIRONMENT}"
                    }
                    // Set environment variables
                    env.AWS_REGION = envProps.AWS_REGION
                    env.ECS_CLUSTER = envProps.ECS_CLUSTER
                    env.ECS_SERVICE = envProps.ECS_SERVICE
                    
                    sh 'printenv'
                }
            }
        }

    }
}
