pipeline {
    agent any

    environment {
        // Define environment variables
        DOCKER_REGISTRY = 'your-docker-registry'
        DOCKER_CREDENTIALS_ID = 'your-docker-credentials-id'
        KUBERNETES_CREDENTIALS_ID = 'your-kubernetes-credentials-id'
        KUBERNETES_CLUSTER_URL = 'https://your-kubernetes-cluster-url'
        IMAGE_NAME = 'your-nodejs-app'
        IMAGE_TAG = 'latest'
        NAMESPACE = 'your-namespace'
    }

    stages {
        stage('Clone code from GitHub') {
            steps {
                script {
                    git 'https://github.com/your-repo/your-nodejs-app.git'
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withKubeConfig([credentialsId: "${KUBERNETES_CREDENTIALS_ID}", serverUrl: "${KUBERNETES_CLUSTER_URL}"]) {
                        sh """
                        kubectl set image deployment/${IMAGE_NAME} ${IMAGE_NAME}=${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} --namespace=${NAMESPACE}
                        kubectl rollout status deployment/${IMAGE_NAME} --namespace=${NAMESPACE}
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                cleanWs()
            }
        }
    }
}
