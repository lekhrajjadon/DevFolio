pipeline {
    agent any

    environment {
        SSH_USER = "azureuser"
        SSH_HOST = "172.174.42.22"
        SSH_KEY = "/var/lib/jenkins/.ssh/id_rsa"
        APP_DIR = "/var/www/html"
        GIT_REPO = "https://github.com/lekhrajjadon/DevFolio.git"
    }

    stages {
        stage('Clone Repository on Application VM') {
            steps {
                script {
                    sh """
                    ssh -i $SSH_KEY -o StrictHostKeyChecking=no $SSH_USER@$SSH_HOST << EOF
                        cd $APP_DIR
                        git pull origin master || git clone $GIT_REPO .
                    EOF
                    """
                }
            }
        }

        stage('Restart Nginx') {
            steps {
                script {
                    sh """
                    ssh -i $SSH_KEY -o StrictHostKeyChecking=no $SSH_USER@$SSH_HOST << EOF
                        sudo systemctl restart nginx
                    EOF
                    """
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

