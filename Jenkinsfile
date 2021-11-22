pipeline {
    agent {
        docker { image 'node:16' }
    }
    stages {
        stage('Image Build') {
            parallel{
                stage('Front-End checkout') {
                    steps {
                        dir('frontend') {
                            git url: 'https://github.com/jang2162/jang2162-frontend-start.git'
                            sh 'npm install'
                        }
                    }
                }
                stage('Back-End checkout') {
                    steps {
                        dir('backend') {
                            git url: 'https://github.com/jang2162/jang2162-backend-start.git'
                            sh 'npm install'
                        }
                    }
                }
            }
        }
    }
}
