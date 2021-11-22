pipeline {
    agent {
        docker { image 'node:16' }
    }
    stages {
        stage('Image Build') {
            parallel{
                stage('Front-End checkout') {
                    dir('frontend') {
                        steps {
                            git url: 'https://github.com/jang2162/jang2162-frontend-start.git'
                            sh 'npm install'
                        }
                    }
                }
                stage('Back-End checkout') {
                    dir('backend') {
                        steps {
                            git url: 'https://github.com/jang2162/jang2162-backend-start.git'
                            sh 'npm install'
                        }
                    }
                }
            }
        }
    }
}
