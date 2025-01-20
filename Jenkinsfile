pipeline {
    environment {
        dockerImage = "minipuppeteer/nginx-proxy"
        dockerTag = "latest"
        dockerHost = "127.0.0.1"
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
                    sh "docker -H ${dockerHost} build -t ${dockerImage}:${dockerTag} ."
                }
            }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh "docker -H ${dockerHost} push ${dockerImage}:${dockerTag}"
            }
        }
    }
}