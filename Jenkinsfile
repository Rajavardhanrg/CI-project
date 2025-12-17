pipeline {
    agent any

    tools {
        jdk 'java-11'
        maven 'maven'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Rajavardhanrg/CI-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t Rajavardhanrg/ci-app:1 .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop c1 || true
                docker rm c1 || true
                docker run -d --name c1 -p 9000:8080 Rajavardhanrg/ci-app:1
                '''
            }
        }
    }
}
