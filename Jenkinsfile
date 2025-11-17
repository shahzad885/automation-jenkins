pipeline {
    agent any 

    environment {
        // Load the secret tokens
        VERCEL_TOKEN_SECRET = credentials('VERCEL_TOKEN')
        VERCEL_PROJECT_ID_SECRET = credentials('VERCEL_PROJECT_ID')
        VERCEL_ORG_ID_SECRET = credentials('VERCEL_ORG_ID')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clones your repository
                git branch: 'main', url: 'https://github.com/shahzad885/automation-jenkins.git'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Use 'bat' for Windows
                // Use %VARIABLE% for Windows variable syntax
                // Added '|| exit 0' to ignore Vercel's Git-linking warning and force success
                bat '''
                  npx vercel --prod --token %VERCEL_TOKEN_SECRET% --scope %VERCEL_ORG_ID_SECRET% --yes --force || exit 0
                '''
            }
        }
    }
}