pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html"
        REPO_URL = "https://github.com/lekhrajjadon/DevFolio.git"
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    sh "sudo rm -rf ${DEPLOY_DIR}/*"
                    sh "sudo git clone ${REPO_URL} ${DEPLOY_DIR}"
                }
            }
        }

        stage('Set Permissions') {
            steps {
                script {
                    sh "sudo chown -R jenkins:www-data ${DEPLOY_DIR}"
                    sh "sudo chmod -R 775 ${DEPLOY_DIR}"
                }
            }
        }

        stage('Restart Web Server') {
            steps {
                script {
                    sh "sudo systemctl restart nginx || sudo systemctl restart apache2"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment successful! 🚀"
        }
        failure {
            echo "Deployment failed! ❌"
        }
    }
}

