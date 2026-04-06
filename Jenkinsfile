pipeline {
 agent { label 'demo' }
 parameters {
     password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Github password')
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
     choice(name:'environment', choices: ['functional', 'integration', 'regression', 'uat', 'release' ] ,description: 'select where need to deploy')
 }
 stages {
  stage('Deploy')
  {
    steps { 
        git branch: 'springboot', credentialsId: 'GithubCred', url: 'https://github.com/rajaraovarre/SpringBoot-Deployment-Pipeline.git'
      dir ("./${params.environment}") {
              sh "sed -i 's/image: adamtravis.*/image: adamtravis\\/democicd:$IMAGETAG/g' deployment.yml" 
	    }
	    sh 'git commit -a -m "New deployment for Build $IMAGETAG"'
	    sh "git push origin springboot"
    }
  }
 }
}
