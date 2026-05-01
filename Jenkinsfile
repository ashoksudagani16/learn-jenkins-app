pipeline {
    agent any

    stages {
        stage('Test') {
            agent {
                docker {
                    image "node:18-alpine"
                    reuseNode true
                }
            }
            steps {
                sh '''
                node -v
                npm ci
                npm test
                '''
            }
        }
         stage('Build') {
            agent {
                docker {
                    image "node:18-alpine"
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm run build
                ls -la
                '''
            }
        }
    }
}
