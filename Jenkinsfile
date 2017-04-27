#!groovy
pipeline {
        agent any

        options{
                buildDiscarder(logRotator(numToKeepStr:'1'))
                skipDefaultCheckout()
        }

        stage('Checkout'){
                steps{
                        checkout scm
                }
        }

        stage ('Test'){
                steps{
                        sh 'docker-compose up -d'
                        sh 'docker-compose run dockerapp python test.py'
                }
        }
}
