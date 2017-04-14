#!groovy
node {
        stage 'Checkout'
        checkout scm

        stage 'Test'
        sh 'docker-compose up -d'
        sh 'docker-compose run dockerapp python test.py'
}
