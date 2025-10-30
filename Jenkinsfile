pipeline {
    agent any 
    stages {
        stage("Build Docker Image") {
            steps {
                echo "Build docker image"
                bat 'docker build -t kubedemoapp:v1 .'
            }
        }
        stage("Docker Login") {
            steps {
                bat 'docker login -u varshap25 -p Varsha@2503'
            }
        }
        stage("Push Docker image to Docker Hub") {
            steps {
                echo "Push docker image to docker hub"
                bat 'docker tag kubedemoapp:v1 varshap25/kuber:version1'
                bat 'docker push varshap25/kuber:version1'
            }
        }
        stage("Deploy to Kubernetes") {
            steps {
                echo "Deploying to kubernetes"
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
    post {
        success {
            echo "Pipeline completed successfully!"
        } 
        failure {
            echo "Pipeline Failed! Please check the logs"
        }
    }
}