pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/P-gupta981/devops-cicd-project.git'
            }
        }

         /*
        stage('Build Docker Image') {
            steps {
               sh 'docker build -t priyagupt/devops-app:latest .' 
            }
        }
      */
        stage('Login Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
            sh 'docker tag devops-app priyagupt/devops-app:latest'
               sh 'docker push priyagupt/devops-app:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yml'
                sh 'kubectl apply -f service.yml'
            }
        }
    }
}
