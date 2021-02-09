pipeline {
    agent any
    
    options{
        ansiColor('xterm')
    }

    tools{
        nodejs "nodejs-14.15.4"
    }

    stages{ 
        stage('Build') {
            steps {
                sh 'yarn'
            }
        }

        stage('test') {
            steps {
                sh 'yarn run test'
            }
        }

        stage('ci-test') {
            steps {
                sh 'yarn run ci-test'
            }
            post {
                always {
                    archiveArtifacts 'coverage/'
                    step([$class: "TapPublisher", testResults: "test.tap"])
                    step([$class: 'CloverPublisher',
                        cloverReportDir: 'coverage/',
                        cloverReportFileName: 'clover.xml',
                        healthyTarget: [methodCoverage: 70, conditionalCoverage: 80, statementCoverage: 80], // optional, default is: method=70, conditional=80, statement=80
                        unhealthyTarget: [methodCoverage: 50, conditionalCoverage: 50, statementCoverage: 50], // optional, default is none
                            failingTarget: [methodCoverage: 0, conditionalCoverage: 0, statementCoverage: 0]     // optional, default is none
                            ])


                }
            }

        }
        stage('Security') {
            steps {
                sh 'trivy filesystem . --format json --output trivy-results.json'
            }
            post {
                always {
                    recordIssues(
                        enabledForFailure: true,
                        tool: trivy(pattern: 'trivy-results.json')
                    )
                }
            }
        }

    }
}
