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
                    // Даем права на Docker socket
                    sh 'sudo chown jenkins:jenkins /var/run/docker.sock'
                    
                    // Собираем и запускаем с нужными правами
                    sh '''
                        docker build -t playwright-tests .
                        docker run \
                            --rm \
                            --network host \
                            --security-opt seccomp=unconfined \
                            --cap-add=SYS_ADMIN \
                            playwright-tests
                    '''
                }
            }
        }
    }
}
