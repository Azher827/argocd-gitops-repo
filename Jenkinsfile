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
                   
                }
                }
            }
        }
    }
}
