//SCRIPTED

//DECLARATIVE
pipeline {
    //agent any
    //agent { docker { image 'maven:3.6.3'}}
    agent { docker { image 'node:13.8'}}
    stages {
        stage('Build') {
            steps {
                //sh "mvn --version"
                sh "node --version"
                echo "Build Stage"
            }
        }
        stage('test') {
            steps {
                echo "test Stage"
            }
        }
        stage('Integration test') {
            steps {
                echo "Integration test Stage"
            }
        }
    }
    post{
        always{
            echo "i indeed do run always"
        }
        success{
            echo "i run only when successful"
        }
        failure{
            echo "i run only when failed"
        }
    }
}
