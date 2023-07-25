pipeline {
    agent any
    environment {
        PATH=sh(script:"echo $PATH:/var/lib/jenkins/apache-maven-3.8.5/bin", returnStdout:true).trim()
    }
    stages {
        stage('Package App With Maven') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t 2807191453/hello-world ."
            }
        }
        stage('Push Images to Docker Repo') {
            steps {
                sh "docker push 2807191453/hello-world"
            }
        }
        stage('Deploy App on Kubernetes'){
            steps {
                sh "kubectl apply -f kubernetes"
            }
        }
    }
    post {
        always {
            sh 'docker image prune -af'
        }
    }
}
