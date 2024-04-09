pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Lint Dockerfile') { 
            when {
                branch 'karsajobs-ui'
            }
            steps {
                sh 'npm install hadolint && hadolint Dockerfile'
            }
        }
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Build and Push Docker Image') { 
            when {
                branch 'karsajobs-ui'
            }
            steps {
                script {
                    // Build and push Docker image here
                    sh 'docker build -t your-image-name .'
                    sh 'docker push your-image-name'
                }
            }
        }  
    }
}
