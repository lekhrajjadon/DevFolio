pipeline {
    agent any

    stages {
        stage('Clone Repository on Application VM') {
            steps {
                script {
                    // SSH into the Azure VM and reset the repository
                    sh '''
                    ssh -i /var/lib/jenkins/.ssh/id_rsa -o StrictHostKeyChecking=no azureuser@172.174.42.22 <<EOF
                    sudo git config --global --add safe.directory /var/www/html
                    cd /var/www/html
                    sudo git reset --hard HEAD  # Discard local changes
                    sudo git clean -fd  # Remove untracked files
                    sudo git pull origin master
                    EOF
                    '''
                }
            }
        }

        stage('Restart Nginx') {
            steps {
                script {
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
            echo "✅ Deployment Successful!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}

