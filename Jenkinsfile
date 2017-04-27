#!groovy
pipeline {
        agent any
        options{
                buildDiscarder(logRotator(numToKeepStr:'1'))
                skipDefaultCheckout()
        }
        stage('Checkout'){
                steps{
                        script{
                                checkout scm
                        }
                }
        }
        stage('Test'){
                agent{
                        image 'docker/compose:1.12.0'
                        label 'test-ci'
                }
                steps{
                        sh 'docker-compose up -d'
                        sh 'docker-compose run dockerapp python test.py'
                        sh 'docker-compose down'
                }
        }
}