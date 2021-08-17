def DOCKER_IMAGE_NAME="samsung-sds:5000/gitopspoc:v${CURRENT_BUILD}"
pipeline {
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
                    sh "echo ${DOCKER_IMAGE_NAME}"
                    sh "yq e -i '.spec.template.spec.containers.[0].image = \"${DOCKER_IMAGE_NAME}\"' ui-deployment.yaml"
                    withCredentials([gitUsernamePassword(credentialsId: 'e65da257-c14c-422d-8383-0be7e96d5763', gitToolName: 'Default')])
                    {
                        sh 'git add ui-deployment.yaml'
                        sh 'git commit -m "changes for new version $IMAGE_NAME"'
                        sh 'git push'
                    }
                }
                }
            }
        }
    }
}
