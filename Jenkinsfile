pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x' // Change as needed
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/mern-app.git'
            }
        }

        stage('Setup Node.js') {
            steps {
                script {
                    def nodeInstalled = sh(script: 'node -v', returnStatus: true) == 0
                    if (!nodeInstalled) {
                        sh 'curl -fsSL https://deb.nodesource.com/setup_$NODE_VERSION | bash -'
                        sh 'apt-get install -y nodejs'
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'cd client && npm install && npm run build'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'pm2 restart server.js || pm2 start server.js --name mern-app'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed! Check logs for details.'
        }
    }
}
