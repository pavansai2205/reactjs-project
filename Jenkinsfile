// pipeline {
//     agent any

//     stages {
//         stage('Clone Repo') {
//             steps {
//                 // Clone directly to the workspace root
//                 git branch: 'master', url: 'https://github.com/pavansai2205/reactjs-project.git'
//             }
//         }

//         stage('Build Docker Images') {
//             steps {
//                 sh 'docker-compose build'
//             }
//         }

//         stage('Start Containers') {
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
        IMAGE_NAME = 'pavansai2205/portfolio_docker-frontend:latest'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/pavansai2205/reactjs-project.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Start Containers') {
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

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker tag portfolio_docker-frontend:latest $IMAGE_NAME
                        docker push $IMAGE_NAME
                        docker logout
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up containers...'
            sh 'docker-compose down || true'
        }
    }
}
