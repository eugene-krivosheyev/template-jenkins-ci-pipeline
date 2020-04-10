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
            
            steps {
                echo 'build-test...'
            }  
        }
        
        stage('sonar') {
            agent { label 'master' }
            
            steps {
                echo 'sonar...'
            }              
        }
        
        stage('publish') {
            agent { label 'master' }
            
            steps {
                echo 'publish...'
            }              
        }
        
        stage('deploy') {
            agent { label 'prod' }
            
            options {
                skipDefaultCheckout true
            }            
            
            steps {
                echo 'deploy...'
            }              
        }
    }
}
