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
  - name: ubuntu
    image: ubuntu:latest
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
            defaultContainer 'ubuntu'
        }
    }
    stages {
        stage('Return Hostname') {
            steps {
                sh 'hostname'
            }
        }
        stage('Run Parallel Executions') {
            /* Begin Parallel Stages */
            parallel {
                stage('Find files > 1Gig') {
                    steps {
                        sh 'find / -type f -size +1G'
                    }
                }
                stage('List all files and directories') {
                    steps {
                        sh "find / -print | sort|sed -e 's;[^/]*/;|____;g;s;____|; |;g'"
                    }
                }
            }
            /* End Parallel Stages */
        }
        stage('End of Run') {
            steps {
                sh 'End of Execution!'
            }
        }
    }
}
