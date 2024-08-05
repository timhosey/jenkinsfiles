// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: maven
    image: maven
    command:
    - sleep
    args:
    - infinity
'''
            // Also can create a Kubernetes Pod Template and reference it instead of YAML

            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
            defaultContainer 'maven'
        }
    }
    stages {
        stage('Test Maven Version') {
            steps {
                sh 'mvn --version'
            }
        }
        stage('Checkout Maven code') {
            steps {
                // checkout sample Maven project
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jenkins-docs/simple-java-maven-app.git']])
            }
        }
        stage('Build Maven project') {
            steps {
                // build Maven
                sh 'mvn clean verify package'
            }
        }
        stage('JUnit test') {
            steps {
                // show directories
                sh 'ls -al ./target'
                sleep 200
            }
        }
        stage('Archive Maven artifact') {
            steps {
                // archive artifact
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
    }
}
