pipeline {
    agent none

    stages {
        stage('clean') {
            agent { label 'agent' }
            
            steps {
                echo 'clean...'
            }            
        }
        
        stage('build-test') {
            agent { label 'agent' }
            options { skipDefaultCheckout true }            
            
            steps {
                echo 'build-test...'
            }  
        }
        
        stage('sonar') {
            agent { label 'agent' }
            options { skipDefaultCheckout true }            
            
            steps {
                echo 'sonar...'
            }              
        }
        
        stage('publish') {
            agent { label 'agent' }
            options { skipDefaultCheckout true }
            
            steps {
                echo 'publish...'
            }              
        }

        stage('deploy-db-schema') {
            agent { label 'prod' }
            options { skipDefaultCheckout true }

            steps {
                echo 'deploy-db-schema...'
            }
        }

        stage('deploy-application') {
            agent { label 'prod' }
            options { skipDefaultCheckout true }
            
            steps {
                echo 'deploy-application...'
            }              
        }
    }
}
