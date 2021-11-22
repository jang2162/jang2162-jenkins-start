pipeline {
    agent {
        docker { image 'node:16' }
    }
    stages {
        stage('Front-End checkout') {
            steps {
                git url: 'https://github.com/jang2162/jang2162-frontend-start.git'
            }
        }
        stage('Back-End checkout') {
            steps {
                git url: 'https://github.com/jang2162/jang2162-backend-start.git'
            }
        }
    }
}
