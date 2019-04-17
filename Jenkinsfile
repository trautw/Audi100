pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
    stages {
        stage('Test1') {
            steps {
                sh 'node --version'
            }
        }
    }
}
