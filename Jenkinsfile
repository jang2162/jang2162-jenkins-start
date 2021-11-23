pipeline {
    agent {
        docker {
            image 'node:16'
            args '-v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker'
        }
    }
    stages {
        stage('Image Build') {
            parallel{
                stage('Front-End') {
                    steps {
                        dir('frontend') {
                            git url: 'https://github.com/jang2162/jang2162-frontend-start.git'
                            script {
                                def commit_id = sh(returnStdout: true, script: 'git rev-parse HEAD')
                                docker.build("jang2162-frontend-start:${commit_id}", './')
                            }
                        }
                    }
                }
                stage('Back-End') {
                    steps {
                        dir('backend') {
                            git url: 'https://github.com/jang2162/jang2162-backend-start.git'
                            script {
                                def commit_id = sh(returnStdout: true, script: 'git rev-parse HEAD')
                                docker.build("jang2162-backend-start:${commit_id}", './')
                            }
                        }
                    }
                }
            }
        }
    }
}
