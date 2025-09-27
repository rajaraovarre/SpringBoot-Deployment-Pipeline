pipeline {
  agent any
  parameters {
    password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
    string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
    choice(name:'environment', choices: ['functional', 'integration', 'regression', 'uat', 'release'], description: 'select where need to deploy')
  }
  stages {
    stage('Deploy') {
      steps { 
        git branch: 'main', credentialsId: 'GitlabCred', url: 'https://gitlab.com/udaykumar5980/spingboot-cd-pipeline.git'

        dir ("./${params.environment}") {
          sh "sed -i 's|image: adamtravis.*|image: adamtravis/democicd:${IMAGETAG}|g' deployment.yml"
        }

        sh """
          git config user.email "udaykumar5980@example.com"
          git config user.name "udaykumar5980"
        """

        sh """
          if ! git diff --quiet; then
            git commit -am "New deployment for Build ${IMAGETAG}"
            git push https://udaykumar5980:${PASSWD}@gitlab.com/udaykumar5980/spingboot-cd-pipeline.git
          else
            echo "No changes to commit"
          fi
        """
      }
    }
  }
}
