pipeline {
    agent any // Run this pipeline on any available Jenkins agent

    environment {
        // Load the secret token we saved in Jenkins credentials
        // The variable 'VERCEL_TOKEN_SECRET' will contain the actual token.
        VERCEL_TOKEN_SECRET = credentials('VERCEL_TOKEN')
        
        // We also load the Project and Org IDs
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
                // This command is for Linux/macOS agents.
                // If your Jenkins server is on Windows, use: bat 'npm install'
                sh 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                // This command is for Linux/macOS agents.
                // If your Jenkins server is on Windows, use: bat 'npm run build'
                sh 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // This is the key deployment command
                // It uses all three credentials to deploy to the correct project
                sh '''
                  npx vercel --prod --token $VERCEL_TOKEN_SECRET --scope $VERCEL_ORG_ID_SECRET --yes --force
                '''
                // Note: The 'vercel link' we did earlier should have linked your project.
                // This command forces the deployment to that linked project.
            }
        }
    }
}