pipeline {
  agent any
  
  stages {
    stage("Update GIT") {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
            script {
              sh "git config user.email greeshma.productiva@gmail.com"
              sh "git config user.name greeshma"
              sh "cat deployment.yaml"
              sh "sed -i 's+pgreeshma/welpython1.*+pgreeshma/welpython1:${DOCKERTAG}+g' deployment.yaml"
              sh "cat deployment.yaml"
              sh "git add ."
              sh "git commit -m 'Done by Jenkins job changemanifest: ${env.BUILD_NUMBER}'"
              sh "git push http://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git"
            }
          }
        }
      }
    }
  }
}

/*node {
  def app
  
  stages{
    stage("update GIT"){
      script{
        catchError(buildResult: 'SUCCESS', stageResult: 'Failure'){
           withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USSERNAME')]) {
             sh "git config user.email greeshma.productiva@gmail.com"
             sh "git config user.name greeshma"
             sh "cat deployment.yaml"
             sh "sed -i 's+pgreeshma/welpython.*+pgreeshma/welpython:${DOCKERTAG}+g' deployment.yaml"
             sh "cat deployment.yaml"
             sh "git add ."
             sh "git commit -m 'Done by Jenkins job changemanifest: $(env.BUILD_NUMBER)'"
             sh "git push http://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git
           }
        }
      }
    }
  }
}*/
          
