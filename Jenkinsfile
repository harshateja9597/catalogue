pipeline {
    agent {
        node {
           label 'linux' 
        }
    }
    environment{
        packageversion = ''
    }
    }
    options{
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
        
    }
    stages {
        stage('get the version') {
            steps {
                script {
                    def packagejson = readjson file: 'package.json'
                    packageversion = packagejson.version
                    echo "packageversion is : $packageversion"

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
        failure{
            echo 'it runs when pipeline fails'
        }
        success{
            echo 'pipeline runs successfully'
        }
    }
}