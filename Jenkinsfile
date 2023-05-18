
def gv

pipeline {
    agent any
    tools {
        maven 'maven-3.6'
    }
    stages { 
        stage("build jar") {
            steps {
                script {
                    echo "Building the application..."
                    sh "mvn package"
                }
                
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "Building docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "docker build -t alejohnny/demo-app:jma-2.0 ."
                    sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                    sh "docker push alejohnny/demo-app:jma-2.0"
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
            
    }
}