pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                echo "Code successfully checked out."
            }
        }

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
                script {
                    echo "Deploying INSIDE Jenkins container..."
                    def deployDir = "/var/jenkins_home/deploy"

                    sh """
                    mkdir -p ${deployDir}
                    cp -r * ${deployDir}/
                    echo "Deploy done! Files copied to ${deployDir}"
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Build and Deployment SUCCESSFUL!"
        }
        failure {
            echo "Build FAILED!"
        }
    }
}
