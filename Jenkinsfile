@Library('jenkins-shared') _

pipeline {
  
  agent {
    docker { image 'squidfunk/mkdocs-material' }
  }
  
  environment {
    SLACK_CHANNEL_NAME = '#kudos-devops-alerts'
  }
  
  stages {
    
    stage('Init') {
      steps {
        script {
          if(GIT_BRANCH=='origin/master') {
            slack.start()
            deploy = true
          }
        }
      }
      post {
        failure {
          script { env.FAILURE_STAGE = 'Init' }
        }
      }
    }
    
    stage('Deploy') {
      when {
        expression { return deploy }
        steps {
          script {
            echo "Hello"
          }
        }
        post {
          failure {
            script { env.FAILURE_STAGE = 'Deploy' }
          }
        }
      }
    }
    post {
      success {
        script {
          slack.success()
        }
      }
      failure {
        script {
          slack.failure()
        }
      }
    }
  }
}
