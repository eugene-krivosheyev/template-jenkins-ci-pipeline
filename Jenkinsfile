pipeline {
    agent none

    stages {
        stage('clean') {
            agent { label 'master' }
            
            steps {
                echo 'clean...'
            }            
        }
        
        stage('build-test') {
            agent { label 'master' }
            options { skipDefaultCheckout true }            
            
            steps {
                echo 'build-test...'
            }  
        }
        
        stage('sonar') {
            agent { label 'master' }
            options { skipDefaultCheckout true }            
            
            steps {
                echo 'sonar...'
            }              
        }
        
        stage('publish') {
            agent { label 'master' }
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

        stage('pack-container') {
            agent { label 'prod' }
            options { skipDefaultCheckout true }

            steps {
                echo 'pack-container...'
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
