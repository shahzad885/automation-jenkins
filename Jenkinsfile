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
        
        // We have removed the 'Install' and 'Build' stages

        stage('Deploy to Vercel') {
            steps {
                // Use 'bat' for Windows
                // This command will deploy your static files to production
                bat '''
                  npx vercel --prod --token $VERCEL_TOKEN_SECRET --scope $VERCEL_ORG_ID_SECRET --yes --force
                '''
            }
        }
    }
}