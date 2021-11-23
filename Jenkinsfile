pipeline {
    agent {
        docker { image 'node:16' }
    }
    stages {
        stage('Image Build') {
            parallel{
                stage('Front-End') {
                    steps {
                        dir('frontend') {
                            git url: 'https://github.com/jang2162/jang2162-frontend-start.git'
                            sh "git rev-parse --short HEAD > .git/commit-id"
                            def frontend_commit_id = readFile('.git/commit-id').trim()
                            echo 'jang2162-frontend-start commit_id : ${frontend_commit_id}'
                            docker.build("jang2162-frontend-start:${backend_commit_id}", "-f Dockerfile")
                        }
                    }
                }
                stage('Back-End') {
                    steps {
                        dir('backend') {
                            git url: 'https://github.com/jang2162/jang2162-backend-start.git'
                            sh "git rev-parse --short HEAD > .git/commit-id"
                            def backend_commit_id = readFile('.git/commit-id').trim()
                            echo 'jang2162-backend-start commit_id : ${}'
                            docker.build("jang2162-backend-start:${}", "-f Dockerfile")
                        }
                    }
                }
            }
        }
    }
}
