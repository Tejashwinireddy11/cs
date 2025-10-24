pipeline {
    agent any

    stages {
        stage("Build Docker image") {
            steps {
                echo "Building Docker image"
                bat "docker build -t plantcare:v1 ."
            }
        }

        stage("Docker Login") {
            steps {
                echo "Logging into Docker Hub"
                bat "docker login -u tejashwini1108 -p Tejashwini@1108"
            }
        }

        stage("Push Docker image to Docker Hub") {
            steps {
                echo "Pushing Docker image to Docker Hub"
                bat "docker tag plantcare:v1 tejashwini1108/casestudy:latest"
                bat "docker push tejashwini1108/casestudy:latest"
            }
        }

        stage("Deploy to Kubernetes") {
            steps {
                echo "Deploying to Kubernetes cluster"
                // 👇 your files are inside the 'cs' folder in the repo
                bat "kubectl apply -f cs/deployment.yaml --validate=false"
                bat "kubectl apply -f cs/service.yaml"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully"
        }
        failure {
            echo "❌ Pipeline failed. Please check the logs."
        }
    }
}
