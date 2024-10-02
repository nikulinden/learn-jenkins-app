pipeline {
    // agent {
    //     docker {
    //         image 'node:18-alpine'
    //         reuseNode true
    //         }
    // }
    stages {
        stage('Install dependencies ...'){
            steps {
                sh '''
                    echo "Installing dependencies using npm ci ..."
                    npm ci
                '''
            }
        }
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
                sh 'echo "Testing..."'
                sh 'npm test'
                sh 'test -f build/index.html'
            }
        }
    }
    
}