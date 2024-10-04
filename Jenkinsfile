pipeline {
    agent any 

    stages {
        stage('Build') {
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
                    echo "Installing dependencies using npm ci ..."
                    npm ci
                    echo "Building ..."
                    npm run build
                    ls -la
                 '''
            }
        }
        stage('test'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo Testing...
                    # test -f build/index.html
                    npm test
                '''
            }
        }

        stage('E2E'){
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.47.2-noble'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    # Install serve to serve the production build
                    npm install serve
            
                    # Start the app on port 3000 in the background
                    PORT=3000 node_modules/.bin/serve -s build &
            
                    # Check for server readiness, retry for 5 times with 5 seconds delay
                    for i in {1..5}; do
                        curl --fail http://localhost:3000/ && break || sleep 5;
                    done
            
                    # Run Playwright tests
                    npx playwright test
                '''
            }
        }
    }

    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
    
}