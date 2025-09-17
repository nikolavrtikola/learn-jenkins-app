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

         stage('Test Stage') {
             agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            
            steps {
                sh '''
                    echo "Printing from the test stage!!!"
                    test -f build/index.html && echo "File exists" || echo "File missing"
                    npm test
                
                '''
            }
        }

        stage('Deploy Stage') {
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
