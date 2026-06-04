pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/muskan13604/cicd-demo.git'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t muskanyadav1/cicd-demo:v1 .'
            }
        }

        stage('Docker Push') {
            steps {
                bat 'docker push muskanyadav1/cicd-demo:v1'
            }
        }
    }
}