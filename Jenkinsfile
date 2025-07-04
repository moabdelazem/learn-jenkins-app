pipeline{
    agent any

    stages {
        stage ("Build") {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci --cache /tmp/npm-cache

                    npm run build
                    ls -la
                '''
            }
        }
        
        stage ("Test") {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm run test
                '''
            }
        }
    }

    post{
        always {
            junit 'test-results/junit.xml'
        }
    }
}