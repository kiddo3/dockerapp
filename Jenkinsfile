pipeline {
    ws("workspace/${env.JOB_NAME}/${env.BRANCH_NAME}".replace('%2F', '_')) {
        stage 'Test'
        sh 'docker-compose up -d'
        sh 'docker-compose run dockerapp python test.py'
    }
}
