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
                        agent{
                                docker{
                                        image 'docker/compose:1.12.0'
                                        //args  '-v $(pwd):'
                                }
                        }
                        steps{
                                sh 'up -d'
                                sh 'run dockerapp python test.py'
                                sh 'down'
                        }
                }

                stage('Deploy'){
                        parameters{
                                booleanParam(defaultValue: false, description: 'Do deploy to dev?', name: 'doDeploy')
                        }
                        steps{
                                script{
                                        if(params.doDeploy){
                                               echo "DEPLOY!"
                                        }else{
                                                sh "NO DEPLOY"
                                        }
                                }
                        }
                }
        }
}