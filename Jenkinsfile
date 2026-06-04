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
        withCredentials([
            usernamePassword(
                credentialsId: 'dockerhub',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS'
            )
        ]) {
            bat '''
            docker login -u %DOCKER_USER% -p %DOCKER_PASS%
            docker push muskanyadav1/cicd-demo:v1
            '''
        }
    }
}
        stage('Deploy') {
    steps {
        bat 'docker pull muskanyadav1/cicd-demo:v1'
        bat 'docker stop cicd-container || exit 0'
        bat 'docker rm cicd-container || exit 0'
        bat 'docker run -d -p 8084:8084 --name cicd-container muskanyadav1/cicd-demo:v1'
    }
}
    }
}