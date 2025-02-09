pipeline {
    agent any // Or specify a specific agent/node

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Rahul-1999/AI-IMAGE-Generator' // Replace with your repo URL
            }
        }

       stage('Build Frontend') {
            agent any // or specify a label if needed
            steps {
                nodejs(configId: 'NodeJS-22') { // Use the name you configured
                    dir('client') {
                        sh 'npm install'
                        sh 'npm run build'
                    }
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