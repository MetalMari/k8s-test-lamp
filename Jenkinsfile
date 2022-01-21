pipeline {
    agent any
    stages {
        stage("Checkout") {
            steps {
                git branch: "main",
                url: "https://github.com/MetalMari/k8s-test-lamp.git"
            }
        }
        stage("Running containers from dockerhub image") {
            steps {
            sh """
            docker pull rahulwagh17/jhooq-docker-demo:jhooq-docker-demo
            """
            }
        }
        stage("Tag new name") {
            steps {
            sh """
            docker images
            """
            sh """
            docker tag rahulwagh17/jhooq-docker-demo:jhooq-docker-demo metalmari/k8s-test-java:latest
            """
            }
        }
        stage("Pushing new images") {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-cred', url: 'https://index.docker.io/v1/') {
                sh """
                docker push metalmari/k8s-test-java:latest
                """
                }
            }
        }
        stage("Kubernetes deployment"){
            steps {
                sh """
                kubectl apply -f k8s-test-deployment.yml
                """
            }
        }
    }
}