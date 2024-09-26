pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
            }
    }
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
            steps {
                sh 'echo "Testing..."'
                sh 'npm test'
            }
        }
    }
    
}