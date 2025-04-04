pipeline {
    agent any

    stages {
        stage('Clone Repository on Application VM') {
            steps {
                script {
                    sh '''
                    ssh -i /var/lib/jenkins/.ssh/id_rsa -o StrictHostKeyChecking=no azureuser@172.174.42.22 \
                    "sudo git config --global --add safe.directory /var/www/html && \
                    cd /var/www/html && \
                    sudo git reset --hard HEAD && \
                    sudo git clean -fd && \
                    sudo git pull origin master"
                    '''
                }
            }
        }

        stage('Restart Nginx') {
            steps {
                script {
                    sh '''
                    ssh -i /var/lib/jenkins/.ssh/id_rsa -o StrictHostKeyChecking=no azureuser@172.174.42.22 \
                    "sudo systemctl restart nginx"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}

