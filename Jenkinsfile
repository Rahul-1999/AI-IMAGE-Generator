pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x' // Change as needed
        MONGO_URI = credentials('mongodb+srv://rhrahul9480:02Dm14q8mRPSYckA@cluster0.yiz8b.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0') // Store MongoDB URI in Jenkins credentials
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
