#!groovy
pipeline {
        agent any

        options{
                buildDiscarder(logRotator(numToKeepStr:'1'))
                skipDefaultCheckout()
        }
        stages{
                stage('Checkout'){
                        steps{
                                dir('code'){
                                        checkout scm
                                }
                        }
                }
                stage('Test'){
                        /*agent{
                                docker{
                                        image 'docker/compose:1.12.0'
                                        args  '-v /tmp:/tmp'
                                }
                        }*/
                        agent docker
                        steps{
                                sh 'docker-compose up -d'
                                sh 'docker-compose run dockerapp python test.py'
                                sh 'docker-compose down'
                        }
                }
        }
}