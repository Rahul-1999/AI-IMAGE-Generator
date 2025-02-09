pipeline {
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: '' // Replace with your repo URL
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
    }
}