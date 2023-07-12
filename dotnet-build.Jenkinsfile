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
  - name: msbuild
    image: timhosey/msbuild-jenkins-agent
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
            defaultContainer 'msbuild'
        }
    }
    stages {
        stage('Main') {
            steps {
                sh 'dotnet --version'
            }
        }
    }
}
