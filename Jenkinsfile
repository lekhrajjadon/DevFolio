pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    sh 'sudo rm -rf /var/www/html/* || true'
                    sh 'sudo git clone https://github.com/lekhrajjadon/DevFolio.git /var/www/html'
                }
            }
        }

        stage('Set Permissions') {
            steps {
                sh 'sudo chown -R www-data:www-data /var/www/html'
            }
        }

        stage('Restart Web Server') {
            steps {
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}

