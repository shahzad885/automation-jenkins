pipeline {
    agent any 

    environment {
        // Load all three secret tokens
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

        stage('Create Vercel Config') {
            steps {
                // This creates the .vercel directory if it doesn't exist
                bat 'if not exist .vercel mkdir .vercel'
                
                // This dynamically writes our Project and Org IDs into the config file
                bat 'echo {"projectId": "%VERCEL_PROJECT_ID_SECRET%", "orgId": "%VERCEL_ORG_ID_SECRET%"} > .vercel/project.json'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Use 'bat' for Windows and %VARIABLE% syntax
                // I've removed '|| exit 0' so we can see the *true* success or failure
                bat '''
                  npx vercel --prod --token %VERCEL_TOKEN_SECRET% --yes --force
                '''
            }
        }
    }
}