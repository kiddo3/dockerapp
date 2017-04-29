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
                /*stage('Test'){
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
                }*/

                stage('Deploy'){
                        steps{
                                script{
                                        def doDeploy = input message: 'Need some input to continue', parameters: [choice(name: 'RELEASE', choices: 'yes\no', description: 'Deploy to dev1?')]
                                        echo "${doDeploy}"
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