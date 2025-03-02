pipeline {
    agent any

    tools {
        // Install Node.js tool with a specific version
        nodejs 'NodeJS_Latest'
    }
    // environment {
    //     GIT_REPO = 'https://github.com/MayankSaxena23/AI-Image-Generator.git'
    //     BRANCH = 'main'
    // }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Install Client Dependencies') {
            steps {
                // Change to the client directory and install dependencies
                dir('client') {
                    sh 'npm install'
                }
            }
        }

        stage('Build Client') {
            steps {
                // Change to the client directory and run the build command
                dir('client') {
                    sh 'CI=false npm run build'
                }
            }
        }
        stage('Install Backend Dependencies') {
            steps {
                // Change to the backend directory and install dependencies
                dir('server') {
                    sh 'npm install'
                    sh 'export MONGODB_URI=$MONGODB_URI'
                    sh 'export CLOUDINARY_CLOUD_NAME=$CLOUDINARY_CLOUD_NAME'
                    sh 'export CLOUDINARY_API_KEY=$CLOUDINARY_API_KEY'
                    sh 'export CLOUDINARY_API_SECRET=$CLOUDINARY_API_SECRET'
                    sh 'export OPENAI_API_KEY=$OPENAI_API_KEY'
                }
            }
        }

        // stage('Show Git Changes') {
        //     steps {
        //         script {
        //             echo "Recent Git Commits:"
        //             bat 'git log -3 --oneline'
                    
        //             echo "Changed Files in Last Commit:"
        //             bat 'git diff --name-only HEAD~1 HEAD'
        //         }
        //     }
        // }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}