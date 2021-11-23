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
                            script {
                                commit_id = sh(returnStdout: true, script: 'git rev-parse HEAD')
                            }
                            echo "jang2162-frontend-start commit_id : ${commit_id}"
                            docker.build("jang2162-frontend-start:${commit_id}", "-f Dockerfile")
                        }
                    }
                }
                stage('Back-End') {
                    steps {
                        dir('backend') {
                            git url: 'https://github.com/jang2162/jang2162-backend-start.git'
                            script {
                                commit_id = sh(returnStdout: true, script: 'git rev-parse HEAD')
                            }
                            echo "jang2162-backend-start commit_id : ${commit_id}"
                            docker.build("jang2162-backend-start:${commit_id}", "-f Dockerfile")
                        }
                    }
                }
            }
        }
    }
}
