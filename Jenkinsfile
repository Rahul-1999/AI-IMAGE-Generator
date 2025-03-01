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
                    bat 'npm install'
                }
            }
        }

        stage('Build Client') {
            steps {
                // Change to the client directory and run the build command
                dir('client') {
                    bat 'npm run build'
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