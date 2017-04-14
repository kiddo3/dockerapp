#!groovy
node {
      ws("workspace/${env.JOB_NAME}/${env.BRANCH_NAME}".replace('%2F', '_')) {
        stage 'Checkout'
            git([branch: ${env.BRANCH_NAME}])
          
        stage 'Test'
        node {        
            sh 'docker-compose up -d'
            sh 'docker-compose run dockerapp python test.py'
      }
   }
}
