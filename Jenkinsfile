pipeline {
    agent any

    environment {
        VM_USER = 'dav'                      // пользователь на VM
        VM_HOST = '10.10.9.96'               // IP VM
        DEPLOY_DIR = '~/deploy'              // куда копируем файлы на VM
    }

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
                    echo "Deploying to VM ${VM_HOST}..."
                    
                    // sshagent — использует ключ из Jenkins Credentials
                    sshagent(['jenkins_vm_ssh_key']) {
                        sh """
                            ssh ${VM_USER}@${VM_HOST} 'mkdir -p ${DEPLOY_DIR}'
                            scp -r * ${VM_USER}@${VM_HOST}:${DEPLOY_DIR}/
                            ssh ${VM_USER}@${VM_HOST} 'echo "Deploy done!"'
                        """
                    }
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
