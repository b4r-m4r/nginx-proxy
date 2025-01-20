pipeline {
    environment {
        dockerImage = "minipuppeteer/nginx-proxy"
        dockerTag = "latest"
        DOCKER_HOST = "127.0.0.1"
    }
    agent any

    stages {
        stage('Login') {
            environment {
                DOCKER_CRDS = credentials('dh_id')
            }
            steps {
                sh('echo $DOCKER_CRDS_PSW | docker login -u $DOCKER_CRDS_USR --password-stdin')
            }
        }
        stage('Build') {
            steps {
                    echo 'Building with local docker daemon...'
                    sh "docker build -t ${dockerImage}:${dockerTag} ."
                }
            }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh "docker push ${dockerImage}:${dockerTag}"
            }
        }
    }
}