pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                dir('react-project') {
                    git branch: 'master', url: 'https://github.com/pavansai2205/reactjs-project.git'
                }
            }
        }

        stage('Build Images') {
            steps {
                dir('react-project') {
                    sh 'docker-compose build'
                }
            }
        }

        stage('Run Containers') {
            steps {
                dir('react-project') {
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Test Containers') {
            steps {
                sh 'docker ps'
            }
        }

    }
}