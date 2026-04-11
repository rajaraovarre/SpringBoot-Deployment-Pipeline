pipeline {
 agent { label 'build' }
 parameters {
     password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Github password')
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
     choice(name:'environment', choices: ['functional', 'integration', 'regression', 'uat', 'release' ] ,description: 'select where need to deploy')
 }
 stages {
  stage('Deploy')
  {
    steps { 
        git branch: 'main', url: 'https://github.com/rajaraovarre/SpringBoot-Deployment-Pipeline.git'
      dir ("kubernetes") {
              sh "sed -i 's|image: razvarre.*|image: razvarre/springbootapp:${IMAGETAG}|g' deployment.yml"
	    }
		sh 'git commit -a -m "New deployment for Build $IMAGETAG"'
	    withCredentials([usernamePassword(credentialsId: 'github-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh "git push https://${USER}:${PASS}@github.com/rajaraovarre/SpringBoot-Deployment-Pipeline.git main"
         }
    }
  }
 }
}
