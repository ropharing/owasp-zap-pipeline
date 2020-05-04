pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                script {
                    startZap(host: "127.0.0.1", port: 8082, timeout:500, allowedHosts:['localhost'], zapHome: "C:\\tools\\owasp\\zap")
                    importZapScanPolicy(policyPath: "C:\\projects\\rob\\owasp-zap-pipeline\\scan.policy")
                }
            }
        }
        stage('Import Urls') {
            steps {
                script {
                    importZapUrls(path: "C:\\projects\\rob\\owasp-zap-pipeline\\rijksoverheid-urls.txt")
                }
            }
        }
        stage('Attack') {
            steps {
                script {
                    runZapAttack(scanPolicyName: "Default Policy")
                }
            }
        }
    }
    post {
        always {
            script {
                archiveZap(failAllAlerts: 0, failHighAlerts: 5, failMediumAlerts: 0, failLowAlerts: 0, falsePositivesFilePath: "zapFalsePositives.json")
            }
        }
    }
}