pipeline {
    agent any

    environment {
        NETLIFY_PROJECT_ID = 'e9a6202c-e98c-4a16-906d-6590146965b1'
    }

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
        stage('Deploy') {
            agent {
                docker {
                    image "node:18-alpine"
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install netlify-cli
                node_modules/.bin/netlify --version
                echo "project id: $NETLIFY_PROJECT_ID"
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
