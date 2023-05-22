#!/usr/bin/env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/aleJohnny/jenkins-shared-library.git',
    credentialsId: 'github-credentials'
    ]
)

pipeline {
    agent any
    tools {
        maven 'maven-3.6'
    }
    environment {
        IMAGE_NAME = "alejohnny/demo-app:java-maven-1.0"
    }
    stages {
        stage("build app") {
            steps {
                script {
                    echo "Building app Jar..."
                buildJar()
                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "Building docker image..."
                    buildImage(env.IMAGE_NAME)
                    dockerLogin()
                    dockerPush (env.IMAGE_NAME)
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "Deploying docker image to EC2..."
                    def shellCmd = "bash ./server-cmds.sh ${IMAGE_NAME}"
                    sshagent(['ec2-server-key']) {
                        sh "scp server-cmds.sh ec2-user@3.72.71.68:/home/ec2-user"
                        sh "scp docker-compose.yaml ec2-user@3.72.71.68:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@3.72.71.68 ${shellCmd}"
                    }
                }
            }
        }
    }   
}