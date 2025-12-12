pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building project..."
                sh "ls -la"
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh "echo Test OK"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying INSIDE Jenkins container..."
                sh '''
                # Папка, куда будем деплоить внутри контейнера Jenkins
                DEPLOY_DIR="/var/jenkins_home/deploy"

                # Создаем директорию, если нет
                mkdir -p $DEPLOY_DIR

                # Копируем ВСЕ файлы из workspace в deploy папку
                cp -r * $DEPLOY_DIR/

                echo "Deploy done! Files copied to $DEPLOY_DIR"
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline finished."
        }
    }
}
