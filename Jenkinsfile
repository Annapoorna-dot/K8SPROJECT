pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Annapoorna-dot/sample'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t myimage /var/lib/jenkins/workspace/kuber'
                sh 'sudo docker tag myimage iammithran/newimage:latest'
                sh 'sudo docker tag myimage iammithran/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push iammithran/newimage:latest'
                sh 'sudo docker image push iammithran/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'kubectl apply -f /var/lib/jenkins/workspace/kuber/pod.yaml'
                sh 'kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
