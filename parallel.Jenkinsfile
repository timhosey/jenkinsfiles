// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            yamlFile 'parallel.yaml'
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
                sh 'hostname; exit 0'
            }
        }
        stage('Run Parallel Executions') {
            /* Begin Parallel Stages */
            parallel {
                stage('List all files larger than 10M') {
                    steps {
                        sh 'find . -type f -size +5M -ignore_readdir_race'
                    }
                }
                stage('List all files and directories') {
                    steps {
                        sh 'ls -R /'
                    }
                }
                stage('Maven') {
                    steps {
                        container('maven') {
                            sh 'mvn --version'
                            // checkout sample Maven project
                            checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jenkins-docs/simple-java-maven-app.git']])
                            // build Maven
                            sh 'mvn clean verify package'
                            // show directories
                            junit stdioRetention: '', testResults: 'target/surefire-reports/*.xml'
                            // archive artifact
                            archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                        }
                    }
                }
            }
            /* End Parallel Stages */
        }
        stage('End of Run') {
            steps {
                echo 'End of Execution!'
            }
        }
    }
}
