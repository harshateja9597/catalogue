pipeline {
    agent {
        node {
            label 'linux'
        }
    }

    environment {
        packageversion = ''
        nexusURL = 'http://52.90.4.99:8081/repository/catalogue/'
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }

    stages {
        stage('Get the Version') {
            steps {
                script {
                    def packagejson = readJSON file: 'package.json'  
                    packageversion = packagejson.version 
                    echo "Package version is: $packageversion" 
                }
            }
        }
        stage('install dependency') {
            steps {
               sh """
                    npm install
               """
            }
        }
        stage('Build') {
            steps {
                sh """
                    ls -la
                    zip -q -r catalogue.zip ./* -x ",*" -x ".zip"
                    ls -ltra 
                    
                """
            }
        }
        stage('publish artifact') {
            steps {
                 nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${nexusURL}",
                    groupId: 'com.roboshop',
                    version: "${packageversion}",
                    repository: 'catalogue',
                    credentialsId: 'nexus-authentication',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
                
            }
        }
    }

    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure {
            echo 'It runs when the pipeline fails'
        }
        success {
            echo 'Pipeline runs successfully'
        }
    }
}
