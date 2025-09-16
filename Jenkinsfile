pipeline {
    agent any
    stages {
        stage('Local Jenkins File') {
            steps {
                sh 'echo "Testing with local Jenkins file"'
                
            }
        }
         stage('Build Stage') {
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
                    npm ci
                    npm run build
                    ls -la

                
                '''
            }
        }
    }
}
