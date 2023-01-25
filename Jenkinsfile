node {
  def app

  stage('Clone repository') {
    checkout scm
  }

  stage('Update GIT') {
    script {
      catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
        withCredentials([usernamePassword(credentialsId: 'bluejuh-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
          sh "git config user.email facefront.letsgo@gmail.com"
          sh "git config user.name FaceFrontLetsGo"
          // sh "git switch master"
          sh "cat vote-ui-deployment.yaml"
          sh "sed -i 's+facefrontletsgo/vote.*+facefrontletsgo/vote:${DOCKERTAG}+g' vote-ui-deployment.yaml"
          sh "cat vote-ui-deployment.yaml"
          sh "git add ."
          sh "git commit -m 'Done by Jenkins Job deployment: ${env.BUILD_NUMBER}'"
          sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/vote-deploy.git HEAD:master"
        }
      }
    }
  }

}
