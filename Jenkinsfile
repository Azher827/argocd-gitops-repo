pipeline {
    parameters {
      string 'DOCKER_IMAGE_NAME'
    }
    agent any
    stages
    {
        stage('Update: GitOps Repo')
        {
            steps
            {
                script
                {
                dir('config')
                {
                    sh "yq e -i '.spec.template.spec.containers.[0].image = \"${DOCKER_IMAGE_NAME}\"' ui-deployment.yaml"
                    withCredentials([gitUsernamePassword(credentialsId: 'e65da257-c14c-422d-8383-0be7e96d5763', gitToolName: 'Default')])
                    {
                        sh 'git config --global push.default simple'
                        sh 'git add ui-deployment.yaml'
                        sh 'git commit -m "changes for new version ${DOCKER_IMAGE_NAME}"'
                        sh 'git push origin HEAD:main'
                    }
                }
                }
            }
        }
    }
}
