pipeline {
    agent {
      label 'master'
    }

    stages {
        stage('add-agent') {
            steps {
                script {
                    jenkins_user="tim"
                    jenkins_token="11653c54508fbd3050b513f253a2edc557"
                    jenkins_url="https://ci.tim.ps.beescloud.com/demo-controller"
                }
                // sh """curl -L -s -w "%{http_code}" -u $jenkins_user:$jenkins_token \\
                // -H "Content-Type:application/x-www-form-urlencoded" -X POST \\
                // -d "json=\$(cat assets/agent.json)" \\
                // "$jenkins_url/computer/doCreateItem"; \\
                // echo"""

                sh """curl -v -XPOST -u $JENKINS_USER_ID:$JENKINS_API_TOKEN -H "Content-Type:application/x-www-form-urlencoded" -d 'json={"name": "apiNode2", "nodeDescription": "agent description", "numExecutors": "1", "remoteFS": "/var/jenkins/", "labelString": "nodeLabel", "mode": "NORMAL", "": ["hudson.plugins.sshslaves.SSHLauncher", "hudson.slaves.RetentionStrategy$Always"], "launcher": {"stapler-class": "hudson.plugins.sshslaves.SSHLauncher", "$class": "hudson.plugins.sshslaves.SSHLauncher", "host": "fakehost", "credentialsId": "my-cred-id", "port": "22", "javaPath": "", "jvmOptions": "", "prefixStartSlaveCmd": "", "suffixStartSlaveCmd": "", "launchTimeoutSeconds": "", "maxNumRetries": "", "retryWaitTime": ""}, "retentionStrategy": {"stapler-class": "hudson.slaves.RetentionStrategy$Always", "$class": "hudson.slaves.RetentionStrategy$Always"}, "nodeProperties": {"stapler-class-bag": "true"}, "type": "hudson.slaves.DumbSlave"}' "${JENKINS_URL}/computer/doCreateItem?name=apiNode2&type=hudson.slaves.DumbSlave"""
            }
        }
    }
}
