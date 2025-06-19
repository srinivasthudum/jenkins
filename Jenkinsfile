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

        stage('Set Unique Version') {
            steps {
                script {
                    def newVersion = "1.0.${env.BUILD_NUMBER}"
                    sh """
                        jq '.version = "${newVersion}"' package.json > tmp.json && mv tmp.json package.json
                        cat package.json
                    """
                }
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
