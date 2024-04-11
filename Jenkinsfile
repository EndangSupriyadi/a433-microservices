pipeline {
    agent any
    
    stages {
        stage('Lint Dockerfile') {
            when {
                branch 'karsajobs-ui'
            }
            steps {
                script {
                    // Install hadolint
                    sh '''
                        wget -O hadolint https://github.com/hadolint/hadolint/releases/download/v2.3.0/hadolint-Linux-x86_64
                        chmod +x hadolint
                    '''
                    // Run hadolint on Dockerfile
                    sh './hadolint Dockerfile'
                }
            }
        }
        
        stage('Build and Push Docker Image') {
            when {
                branch 'karsajobs-ui'
            }
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t karsajobs-ui .'
                    
                    // Tag Docker image
                    sh 'docker tag karsajobs-ui:latest karsajobs-ui/karsajobs-ui:latest'
                    
                    // Push Docker image
                    sh 'docker push karsajobs-ui/karsajobs-ui:latest'
                }
            }
        }
    }
}
