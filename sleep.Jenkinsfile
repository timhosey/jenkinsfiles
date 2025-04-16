// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            yamlFile 'sleep.yaml'
            // Also can create a Kubernetes Pod Template and reference it instead of YAML

            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
            defaultContainer 'busybox'
        }
    }
    stages {
        stage('Send Echo') {
            steps {
                echo 'Sleeping job for failover test.'
            }
        }
        stage('Sleep for 5 minutes') {
            steps {
                sleep 300
            }
        }
    }
}
