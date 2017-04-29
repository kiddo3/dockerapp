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
                        steps{
                                script{
                                        input message: 'Need some input', parameters: [booleanParam(defaultValue: false, description: 'Do the deploy?', name: 'doDeploy')]
                                        if(doDeploy){
                                               echo "DEPLOY!"
                                        }else{
                                                echo "NO DEPLOY"
                                        }
                                }
                        }
                }
        }
}