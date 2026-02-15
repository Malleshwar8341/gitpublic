pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/cicd-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t cicd-demo:latest .'
            }
        }

        stage('Push to Registry') {
            steps {
                sh 'docker tag cicd-demo:latest your-dockerhub-user/cicd-demo:latest'
                sh 'docker push your-dockerhub-user/cicd-demo:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
