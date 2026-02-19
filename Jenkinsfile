pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/BangerAtifAhmed/CC_LAB-6.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t backend-image ./backend'
            }
        }

        stage('Remove Old Containers') {
            steps {
                sh 'docker rm -f backend-container || true'
                sh 'docker rm -f nginx-container || true'
            }
        }

        stage('Run Backend Container') {
            steps {
                sh 'docker run -d --name backend-container backend-image'
            }
        }

        stage('Run NGINX Container') {
            steps {
                sh '''
                docker run -d -p 8081:80 --name nginx-container \
                -v $(pwd)/nginx:/etc/nginx/conf.d \
                nginx
                '''
            }
        }

    }
}
