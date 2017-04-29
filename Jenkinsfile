#!groovy
pipeline {
        agent any

        options{
                buildDiscarder(logRotator(numToKeepStr:'1'))
                skipDefaultCheckout()
        }
        environment{
                CURRENT_BUILD = currentBuild.getNumber()
        }
        stages{
                stage('Checkout'){
                        steps{
                                dir('code'){
                                        checkout scm
                                        echo "Current build: ${CURRENT_BUILD}"
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
                                        def props = readJSON file: 'code/dev1.env.json'
                                        echo "Usuario: ${props.user}"
                                        def doDeploy = input message: 'Need some input to continue', parameters: [choice(name: 'Deploy', choices: 'yes\nno', description: 'Deploy to dev1?')]
                                        echo "${doDeploy}"
                                        if(doDeploy == 'yes'){
                                               echo "DEPLOY!"
                                        }else{
                                                echo "NO DEPLOY"
                                        }
                                }
                        }
                }
        }
}