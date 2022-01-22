node {
        
    def  IMAGE_NAME = 'andylee1973/python'    
    def  GIT_TOKEN_ID = 'fstop-andy-lee-github-token'
    def  GIT_USER_MAIL = 'andy_lee@fstop.com.tw'
    def  GIT_USER_NAME = 'fstop-andy-lee'
    def  GIT_HOST = 'github.com'
    def  GIT_BRANCH = 'main'
    def  GIT_REPO = 'python-manifest'
    def  DEPLOY_FILE = 'deployment.yaml'
    

    stage('Clone repository') {
        checkout scm
    }

    stage('Update Manifest') {
      script {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          withCredentials([usernamePassword(credentialsId: GIT_TOKEN_ID, passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
            sh """
                 git config user.email ${GIT_USER_MAIL}
                 git config user.name ${GIT_USER_NAME}
                 sed -i 's+${IMAGE_NAME}.*+${IMAGE_NAME}:${DOCKERTAG}+g' ${DEPLOY_FILE}
                 cat ${DEPLOY_FILE}
                 git add .
                 git commit -m 'Done by Jenkins Job: ${DOCKERTAG}'
                 git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${GIT_HOST}/${GIT_USERNAME}/${GIT_REPO}.git HEAD:${GIT_BRANCH}
               """
               /*
                        sh "git config user.email andy_lee@fstop.com.tw"
                        sh "git config user.name andy_lee"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+andylee1973/python.*+andylee1973/python:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/python-manifest.git HEAD:main"
              */          
          }
        }
      }
    }
}
