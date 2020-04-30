pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                script {
                    startZap(host: "127.0.0.1", port: 8082, timeout:500)
                    importZapUrls(path: "C:\\owasp-zap\\rijksoverheid\\rijksoverheid-urls.txt")
                    importZapScanPolicy(policyPath: "C:\\owasp-zap\\rijksoverheid\\rijksoverheid-policy.policy")
                }

            }
        }
        stage('Build & Test') {
            steps {
                script {
                    sh "mvn verify -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=8082"
                }
            }
        }
    }
}