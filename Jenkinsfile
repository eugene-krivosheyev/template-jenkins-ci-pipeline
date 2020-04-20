pipeline {
    agent none
    options {
        skipDefaultCheckout()
        skipStagesAfterUnstable()
    }

    stages {
        stage('checkout') {
            agent { node { label 'ci' } }

            steps {
                checkout scm
            }
        }

        stage('clean-build-test-qa-publish') {
            agent { node { label 'ci' } }

            steps {
                echo 'sh \'mvn clean deploy\''
            }
            post {
                always {
                    echo 'junit \'target/surefire-reports/*.xml\''
                }
            }
        }


        stage('transfer') {
            agent { node { label 'prod' } }

            steps {
                echo 'sh \'mvn org.apache.maven.plugins:maven-dependency-plugin:2.4:get -Dtransitive=false -Ddest=/opt/app/app.jar.new -DremoteRepositories=artifacts::::http://1.1.1.1.:8081/artifactory/app -Dartifact=com.acme:app:1.0-SNAPSHOT\''
            }
        }

        stage('deploy-db-schema') {
            agent { node { label 'prod' } }

            steps {
                echo 'sh \'mvn liquibase:update\''
            }
        }

        stage('deploy-application') {
            agent { node { label 'prod' } }
            
            steps {
                echo 'sh \'service app stop\''
                echo 'sh \'mv /opt/app/app.jar.new /opt/app/app.jar\''
                echo 'sh \'service app start\''
            }              
        }
    }
}
