node {
        stage("Checkout") {
                git branch: "main",
                url: "https://github.com/MetalMari/k8s-test-lamp.git"
        }
        stage("Running containers from dockerhub image") {
            sh """
            docker pull rahulwagh17/jhooq-docker-demo:jhooq-docker-demo
            """
        }
        stage("Tag new name") {
            sh """
            docker images
            """
            sh """
            docker tag rahulwagh17/jhooq-docker-demo:jhooq-docker-demo metalmari/k8s-test-java:latest
            """
        }
        stage("Pushing new images") {
                withDockerRegistry(credentialsId: 'dockerhub-cred', url: 'https://index.docker.io/v1/') {
                sh """
                docker push metalmari/k8s-test-java:latest
                """
            }
        }
        stage("Kubernetes deployment"){
                sh """
                kubectl apply -f k8s-test-deployment.yml
                """
        }
}