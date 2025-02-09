pipeline {
    agent any // Or specify a specific agent/node

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Rahul-1999/AI-IMAGE-Generator' // Replace with your repo URL
            }
        }

        stage('Build Frontend') {
            steps {
                dir('client') { // Change to your frontend directory
                    sh 'npm install' // Or yarn install
                    sh 'npm run build' // Or yarn build
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir('server') { // Change to your backend directory
                    sh 'npm install' // Or yarn install
                }
            }
        }

        stage('Test') {
            steps {
                dir('client') {
                    sh 'npm test' // Or yarn test
                }
                dir('server') {
                    sh 'npm test' // Or yarn test
                }
            }
        }
    }
}