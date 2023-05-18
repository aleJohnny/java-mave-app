def groovy

pipeline {
    agent any
    parameters {
        string(name: 'VERSION', defaultValue:'2.2', description: '')
    }
    tools {
        maven 'maven-3.6'
    }
    stages {
        stage("init") {
            steps {
                script {
                    groovy = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    groovy.buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    groovy.buildImage()
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    groovy.deployApp()
                }
            }
        }
    }
}