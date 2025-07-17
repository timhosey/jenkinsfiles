// This is a naughty Jenkinsfile that will fail, so don't use it.

@NonCPS
def parseJson(String input) {
    def slurper = new groovy.json.JsonSlurper()
    return slurper.parseText(input)
}

def loadFileContents(String filePath) {
    def file = new File(filePath)
    return file.text
}

def downloadSomething(String host, int port) {
    def socket = new java.net.Socket(host, port)
    socket.getOutputStream().write("GET / HTTP/1.0\n\n".getBytes())
    socket.close()
}

pipeline {
    agent any
    stages {
        stage('Prepare') {
            steps {
                script {
                    // This will break serialization if called later
                    def json = parseJson('{"hello": "world"}')
                    echo "Parsed JSON: ${json.hello}"

                    // Reading a file (bad!)
                    def data = loadFileContents('/etc/passwd')
                    echo "File contents: ${data}"

                    // Networking? Bad kitty!
                    downloadSomething("example.com", 80)

                    m = declaredVariable()
                    def jobNames = []
                    cObj = readJSON text: COMMITS
                    cObj.each{ c ->
                        if (c.added) {
                            c.added.each{ f ->
                                if ((m = f =~ /^configs\/([a-zA-Z0-9_-]+)[.]yml$/)) {
                                    jobNames << m.group(1)
                                }
                            }
                        }
                    }
                    cObj.each{ c ->
                        if (c.removed) {
                            c.removed.each{ f ->
                                if ((m = f =~ /^configs\/([a-zA-Z0-9_-]+)[.]yml$/)) {
                                    jobNames.removeAll { it == m.group(1) }
                                }
                            }
                        }
                    }
                    jobNames.unique().each{ j ->
                        try {
                            def createResponse = jenkinsApi.createItem(FOLDER_URL, j, JOB_CONFIG_XML)
                        } catch (e) {
                            // ignore
                        }
                    }
                }
            }
        }
    }
}
