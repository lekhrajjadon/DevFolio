pipeline {
    agent any

    stages {
        stage('Clone Repository on Application VM') {
            steps {
                script {
                    // SSH into the Azure VM and pull the latest code
                    sh '''
                    ssh -i /var/lib/jenkins/.ssh/id_rsa -o StrictHostKeyChecking=no azureuser@172.174.42.22 <<EOF
                    sudo git config --global --add safe.directory /var/www/html
                    sudo chown -R azureuser:azureuser /var/www/html
                    sudo chmod -R 755 /var/www/html
                    cd /var/www/html
                    git pull origin master
                    EOF
                    '''
                }
            }
        }

        stage('Restart Nginx') {
            steps {
                script {
                    // Restart Nginx service
                    sh '''
                    ssh -i /var/lib/jenkins/.ssh/id_rsa -o StrictHostKeyChecking=no azureuser@172.174.42.22 <<EOF
                    sudo systemctl restart nginx
                    EOF
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}

