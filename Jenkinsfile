pipeline {
    agent any

    stages{ 
        stage('Dependencias') {
            steps {
                sh 'yarn'
            }
        }

        stage('Test') {
            steps {
                sh 'yarn run test'
            }
        }

        stage('ci-Test') {
            steps {
                sh 'yarn run ci-test'
            }
        }
    }
}
