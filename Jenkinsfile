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

        stage ("E2E") {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install -g serve
                    node_modules/.bin/serve -S build &
                    sleep 10
                    npx playwright test
                '''
            }
        }
    }
}