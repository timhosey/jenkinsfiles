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

                sh "curl -v -XPOST -u $jenkins_user:$jenkins_token -H 'Content-Type:application/x-www-form-urlencoded' -d \'json=\$(cat assets/agent.json)\' '$jenkins_url/computer/doCreateItem'"
            }
        }
    }
}
