// pipeline {
//     agent any

//     stages {
//         stage('Clone Repo') {
//             steps {
//                 // Clone directly to the workspace root
//                 git branch: 'master', url: 'https://github.com/pavansai2205/reactjs-project.git'
//             }
//         }

//         stage('Build Images') {
//             steps {
//                 sh 'docker-compose build'
//             }
//         }

//         stage('Run Containers') {
//             steps {
//                 sh 'docker-compose up -d'
//             }
//         }

//         stage('Test Containers') {
//             steps {
//                 sh 'docker ps'
//                 sh 'docker-compose logs frontend'
//             }
//         }
//     }
// }


pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "reactapp"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/pavansai2205/reactjs-project.git'
                sh 'ls -la'  // verify package.json exists
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker-compose down --volumes --remove-orphans || true'
                sh 'docker-compose build --no-cache'
            }
        }

        stage('Start Container') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Wait for App') {
            steps {
                echo 'Waiting 10 seconds for app to start...'
                sh 'sleep 10'
            }
        }

        stage('Check Logs') {
            steps {
                sh 'docker-compose ps'
                sh 'docker-compose logs frontend'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker-compose down --remove-orphans'
        }
    }
}
