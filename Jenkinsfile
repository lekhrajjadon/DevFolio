pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', 
                    url: 'https://github.com/lekhrajjadon/DevFolio.git'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    # Clear destination
                    rm -rf /var/www/html/*
                    
                    # Copy files
                    cp -r . /var/www/html/
                    
                    # Set permissions (works with either permission or sudo approach)
                    chown -R www-data:www-data /var/www/html || true
                    find /var/www/html -type d -exec chmod 755 {} \\; || true
                    find /var/www/html -type f -exec chmod 644 {} \\; || true
                '''
            }
        }

        stage('Restart Web Server') {
            steps {
                sh 'systemctl reload nginx || true'
            }
        }
    }
}
