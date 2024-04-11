pipeline {
    agent any
    
    stages {
        stage('Lint Dockerfile') {
            when {
                branch 'karsajobs'
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
        
        stage('Test App') {
            when {
                branch 'karsajobs'
            }
            steps {
                // Menjalankan unit test untuk backend
                sh 'go test -v -short --count=1 $(go list ./...)'
            }
        }
        
        stage('Build and Push App for Karsajobs') {
            when {
                branch 'karsajobs'
            }
            steps {
                script {
                    // Build dan push image di sini
                    sh 'docker build -t karsajobs-backend .'
                    sh 'docker push karsajobs-backend'
                }
            }
        }
    }
}
