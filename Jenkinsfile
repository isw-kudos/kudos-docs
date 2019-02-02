@Library('jenkins-shared') _

pipeline {
  
  agent {
    docker {
        image 'squidfunk/mkdocs-material'
        args '--entrypoint="" -u=root'
    }
  }
  
  environment {
    SLACK_CHANNEL_NAME = '#kudos-devops-alerts'
    FAILURE_STAGE = 'Unknown'
    GIT_CREDENTIALS_ID= 'kudos-devops-git'
  }
  
  stages {
    
    stage('Init') {
      steps {
        script {
          deploy = GIT_BRANCH=='origin/master'
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
      }
      steps {
        // script { slack.start() }
        withCredentials([
          usernamePassword(credentialsId: GIT_CREDENTIALS_ID, passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')
        ]) {
          sh '''
          echo "https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com" > .git-credentials
          git config --global credential.helper "store --file=.git-credentials"
          mkdocs gh-deploy
          '''
        }
      }
      post {
        failure {
          script { env.FAILURE_STAGE = 'Deploy' }
        }
      }
    }
  }
  // post {
  //   success {
  //     script {
  //       slack.success()
  //     }
  //   }
  //   failure {
  //     script {
  //       slack.failure()
  //     }
  //   }
  // }
}
