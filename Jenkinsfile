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
                success {
                    archiveArtifacts 'coverage/'
                }
                always{
                    step([$class: "TapPublisher", testResults: "test.tap"])
                    step([$class: 'CloverPublisher',
                    cloverReportDir: 'target/site',
                    cloverReportFileName: 'clover.xml'])
                }

            }
        }
    }
}
