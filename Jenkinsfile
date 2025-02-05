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
                    env.packageversion = packagejson.version 
                    echo "Package version is: ${env.packageversion}" 
                }
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

    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        failure {
            echo 'It runs when the pipeline fails'
        }
        success {
            echo 'Pipeline runs successfully'
        }
    }
}
