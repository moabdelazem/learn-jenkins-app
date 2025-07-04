pipeline{
    agent any

    stages {
        stage ("Build") {
            steps {
                agent {
                    docker {
                        image 'node:alpine-18'
                        reuseNode true
                    }
                }
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci

                    npm run build
                    ls -la
                '''
            }
        }
    }
}