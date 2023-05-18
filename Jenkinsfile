
def gv

pipeline {
    agent any
    tools {
        maven = "maven-3.6"
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
                    echo "Building image..."
                    withCredentials([
                        usernamePassword(credentialsId: 'docker-hub-repo', usernameVariable: 'USER', passwordVariable: 'PASS')
                        ])
                    sh "docker build -t alejohnny/demoapp:jma-2.0"
                    sh "echo ${PASS} | docker login -u ${USER} --password-with-stdin"
                    sh "docker push alejohnny/demoapp:jma-2.0"
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