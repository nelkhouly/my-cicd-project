pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        DOCKER_CONFIG = '/tmp/.docker'
    }

    stages {
        stage('Build Image') {
            steps {
                sh 'mkdir -p $DOCKER_CONFIG'
                sh 'docker build -t my-web-app:latest .'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'docker run --rm my-web-app:latest python3 test_app.py'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker stop my-app-container || true'
                sh 'docker rm my-app-container || true'
                sh 'docker run -d -p 5000:5000 --name my-app-container my-web-app:latest'
            }
        }
    }
}