pipeline {
    agent {
        docker {
            image 'node:16'
            args '-v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker'
        }
    }
    stages {
        stage('Image Build / Push') {
            parallel{
                stage('Front-End') {
                    steps {
                        dir('frontend') {
                            git url: 'https://github.com/jang2162/jang2162-frontend-start.git'
                            configFileProvider([configFile(fileId: 'ENV_FRONT_END_DEV', variable: 'FRONT_END_ENV')]) {
                                sh 'mv $FRONT_END_ENV .env'
                                sh 'npm install && npm run build'
                                script {
                                    def commit_id = sh(returnStdout: true, script: 'git rev-parse HEAD')
                                    def app = docker.build("jang2162/frontend-start")
                                    docker.withRegistry('http://registry') {
                                        echo "==${commit_id}=="
                                        app.push("${commit_id}".trim())
                                        app.push("latest")
                                    }
                                }
                            }
                        }
                    }
                }
                stage('Back-End') {
                    steps {
                        dir('backend') {
                            git url: 'https://github.com/jang2162/jang2162-backend-start.git'
                            configFileProvider([configFile(fileId: 'ENV_BACK_END_DEV', variable: 'BACK_END_ENV')]) {
                                sh 'mv $BACK_END_ENV .env'
                                sh 'npm install && npm run build'
                                script {
                                    def commit_id = sh(returnStdout: true, script: 'git rev-parse HEAD')
                                    def app = docker.build("jang2162/backend-start")
                                    docker.withRegistry('http://registry') {
                                        echo "==${commit_id}=="
                                        app.push("${commit_id}".trim())
                                        app.push("latest")
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
