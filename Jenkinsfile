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
                sh '''echo Testing...
                test -f build/index.html
                npm test
                '''
            }
        }
    }
    
}