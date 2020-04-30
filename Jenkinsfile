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
    post {
        always {
            script {
                archiveZap(failAllAlerts: 1, failHighAlerts: 0, failMediumAlerts: 0, failLowAlerts: 0, falsePositivesFilePath: "zapFalsePositives.json")
            }
        }
    }
}