pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Run Tests') {
            steps {
                script {
                    // Собираем и запускаем тесты в Docker
                    sh '''
                        docker build -t playwright-tests .
                        docker run playwright-tests
                    '''
                }
            }
        }
    }
}
