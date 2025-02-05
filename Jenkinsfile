pipeline {
    agent {
        node {
            label 'linux'
        }
    }

    environment {
        packageversion = ''
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
                    zip -r catalogue.zip ./* -x ",*" -x ".zip"
                    ls -ltra 
                """
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
