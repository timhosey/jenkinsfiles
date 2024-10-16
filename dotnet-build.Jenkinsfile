// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            yamlFile 'dotnet.yaml'
            // Also can create a Kubernetes Pod Template and reference it instead of YAML

            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
            defaultContainer 'msbuild'
        }
    }
    stages {
        stage('Confirm .NET version') {
            steps {
                sh 'dotnet --version'
            }
        }
        stage('Checkout code') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/doddatpivotal/dotnet-hello-world.git']])
            }
        }
        stage('Build project') {
            steps {
                sh 'mkdir out'
                sh 'dotnet build -o ./out'
            }
        }
        stage('Archive artifacts') {
            steps {
                echo '** Listing PWD'
                sh 'ls ./'
                echo '*** Listing ./out'
                sh 'ls ./out'
            }
        }
    }
}
