pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'e884f76b-194e-437e-b6bb-3a3d6e3b0d4e'
        NETLIFY_AUTH_TOKEN = credentials('vdespa-exampe')
    }

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
                  node --version
                  npm --version
                  npm install netlify-cli -g
                  netlify --version
                  echo "deploying to the site ID: $NETLIFY_SITE_ID"
                  netlify status
                  npx netlify deploy --dir=build --prod --no-build
                '''
            }
        }
    }
}
