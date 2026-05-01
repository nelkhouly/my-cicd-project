pipeline {
    agent any
    stages {
        stage('Build Image') {
            steps {
                sh 'docker build -t my-web-app:latest .'
            }
        }
        stage('Run Tests') {
            steps {
                // بنشغل التست جوه الـ Image اللي لسه بنينها
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