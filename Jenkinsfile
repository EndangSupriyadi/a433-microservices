pipeline {
    agent any
    
    stages {
        stage('Lint Dockerfile') {
            when {
                branch 'karsajobs-ui'
            }
            steps {
                script {
                    // Instal hadolint
                    sh '''
                        wget -O hadolint https://github.com/hadolint/hadolint/releases/download/v2.3.0/hadolint-Linux-x86_64
                        chmod +x hadolint
                    '''
                    // Jalankan hadolint terhadap Dockerfile
                    sh './hadolint Dockerfile'
                }
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
                    sh 'docker build -t karsajobs-ui .'
                    sh 'docker push karsajobs-ui'
                }
            }
        }
    }
}
