pipeline {
    agent any

    environment {
        VERDACCIO_REGISTRY = 'http://localhost:4873'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Pack the Module') {
            steps {
                sh 'npm pack'
            }
        }

        stage('Publish to Verdaccio') {
            steps {
                sh 'npm publish --registry=${VERDACCIO_REGISTRY}'
            }
        }
    }
}
