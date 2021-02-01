pipeline {
    agent any
    tools{
        nodejs "NodeJS"
    }

    stages{ 
        stage('Dependencias') {
            steps {
                sh 'npm install'
            }
        }

        stage('test') {
            steps {
                sh 'npm run test'
            }
        }

        stage('ci-test') {
            steps {
                sh 'npm run ci-test'
            }
            post {
                success {
                    archiveArtifacts 'coverage/'
                }
            }
        }
    }
}
