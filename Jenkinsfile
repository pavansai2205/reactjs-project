pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                // Clone directly to the workspace root
                git branch: 'master', url: 'https://github.com/pavansai2205/reactjs-project.git'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Test Containers') {
            steps {
                sh 'docker ps'
                sh 'docker-compose logs frontend'
            }
        }
    }
}
