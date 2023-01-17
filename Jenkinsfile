//SCRIPTED

//DECLARATIVE
pipeline {
    agent any
    //agent { docker { image 'maven:3.6.3'}}
    //agent { docker { image 'node:13.8'}}
    environment {
        dockerLoko = tool 'myDocker'
        mavenLoko = tool 'myMaven'
        PATH = "$dockerLoko/bin:$mavenLoko/bin:$PATH"
    
    }
    stages {
        stage('Checkout') {
            steps {
                sh "mvn --version"
                sh "docker version"
                sh "docker images ls"
                echo "Build Stage"
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD_ID - $env.BUILD_ID"
                echo "JOB_NAME - $env.JOB_NAME"
                echo "BUILD_TAG - $env.BUILD_TAG"
                echo "BUILD_URL - $env.BUILD_URL"
                echo "EXECUTOR_NUMBER - $env.EXECUTOR_NUMBER"
            }
        }
        stage('Build & Compile') {
            steps {
                sh "mvn clean compile"
                echo "compile was Good"
            }
        }
        
        stage('test') {
            steps {
                sh "mvn test"
                echo "testing all good"
            }
        }
        
        stage('Integration test') {
            steps {
                sh "mvn failsafe:Integration-test failsafe:verify"
                echo "int-test and verification approved"
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
