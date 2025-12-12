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
                echo "Deploy stage triggered..."
                sh "echo Deploy Done"
            }
        }
    }

    post {
        always {
            echo "Pipeline finished."
        }
    }
}
