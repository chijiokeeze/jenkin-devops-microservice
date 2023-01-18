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
                sh "mvn failsafe:integration-test failsafe:verify"
                echo "int-test and verification approved"
            }
        }
        stage('Package app') {
            steps {
                sh "mvn package -DskipTests"
                echo "int-test and verification approved"
            }
        }
       stage('Building Docker image') {
            steps {
                //"docker build -t cj15/jenkin_devops_microservice:$env.BUILD_TAG"
                script {
                    dockerImage = docker.build("cj15/jenkin_devops_microservice:${env.BUILD_TAG}")
                }
                echo "at this point docker image has been built"
            }
        }
       stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhubpass') {
                        dockerImage.push();
                        dockerImage.push('latest');
                    }
                   
                }
                echo "docker image with build tag ${env.BUILD_TAG} has been pushed!!!"
            }
        }
    }
}	
