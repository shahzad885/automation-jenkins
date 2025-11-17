pipeline {
    // Run this pipeline on any available Jenkins agent
    agent any 

    environment {
        // Load the secret tokens we saved in Jenkins credentials
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
        
        stage('Install Dependencies') {
            steps {
                // Use 'bat' for Windows instead of 'sh'
                bat 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                // Use 'bat' for Windows instead of 'sh'
                bat 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Use 'bat' for Windows instead of 'sh'
                // This command deploys to production using our three credentials
                bat '''
                  npx vercel --prod --token $VERCEL_TOKEN_SECRET --scope $VERCEL_ORG_ID_SECRET --yes --force
                '''
            }
        }
    }
}