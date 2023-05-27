pipeline {
    def app

    stage('Clone the repository') {
        git branch: 'main', url: 'https://github.com/adityamurali155/kubernetesmanifest.git'
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                    sh "git config user.email ${USER_EMAIL}"
                    sh "git config user.name ${USER_NAME}"
                    //sh "git switch master"
                    sh "sed -i 's+${USER_NAME}/myapp.*+stoneherc/myapp:${DOCKERTAG}+g' deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                    
                }
            }
        }
    }
}
