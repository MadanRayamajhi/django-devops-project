pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/MadanRayamajhi/django-devops-project.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t django-app .'
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker stop django-app || true'
                sh 'docker rm django-app || true'
                sh 'docker run -d --name django-app -p 8000:8000 django-app'
            }
        }

        stage('Test API') {
            steps {
                sh 'sleep 5'
                sh 'curl -f http://localhost:8000 || exit 1'
            }
        }
    }

    post {
        success {
            echo '✅ Django Deployment Successful!'
        }
        failure {
            echo '❌ Django Pipeline Failed!'
        }
    }
}
