pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/lekhrajjadon/DevFolio.git', 
                     branch: 'master'
            }
        }
        
        stage('Deploy') {
            steps {
                sh '''
                    ssh -o StrictHostKeyChecking=no  azureuser@172.174.42.22 \
                    "sudo git -C /var/www/html pull origin main"
                '''
            }
        }
    }
}
