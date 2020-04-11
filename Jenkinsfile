pipeline {
    agent none
    options {
        skipDefaultCheckout()
        skipStagesAfterUnstable()
    }

    stages {
        stage('checkout') {
            agent { node { label 'agent' } }

            steps {
                checkout scm
            }
        }

        stage('clean-build-test-qa-publish') {
            agent { node { label 'agent' } }

            steps {
                sh 'mvn clean deploy'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }


        stage('transfer') {
            agent { node { label 'prod' } }

            steps {
                sh 'mvn org.apache.maven.plugins:maven-dependency-plugin:2.4:get -Dtransitive=false -Ddest=/opt/app/app.jar.new -DremoteRepositories=artifacts::::http://1.1.1.1.:8081/artifactory/app -Dartifact=com.acme:app:1.0-SNAPSHOT'
            }
        }

        stage('deploy-db-schema') {
            agent { node { label 'prod' } }

            steps {
                sh 'mvn liquibase:update'
            }
        }

        stage('deploy-application') {
            agent { node { label 'prod' } }
            
            steps {
                sh 'service app stop'
                sh 'mv /opt/app/app.jar.new /opt/app/app.jar'
                sh 'service app start'
            }              
        }
    }
}
