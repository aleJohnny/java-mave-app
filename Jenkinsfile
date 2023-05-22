#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application..."
                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    def dockerCmd = "docker run -p 3080:80 -d alejohnny/demo-app:1.0"
                    sshagent(['ec2-server-key']) {
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@3.72.71.68 ${dockerCmd}"
                    }
                }
            }
        }

    }
}