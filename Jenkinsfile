#!/usr/bin/env groovy

@Library('jenkins-shared-library')
def gv

pipeline {
    agent any
    tools {
        maven 'maven-3.6'
    }
    parameters {
        string (name: 'VERSION', defaultValue: '3.0', description: 'Image version')
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    buildImage "alejohnny/demo-app:jma-${params.VERSION}"
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                    //gv.deployApp()
                }
            }
        }
    }   
}