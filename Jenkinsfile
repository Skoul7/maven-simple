node 
{
    stage('Checkout')
      {
        checkout([$class: 'GitSCM', branches: [[name: '${TAG}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Sahil_Koul_github', url: 'https://github.com/Skoul7/maven-simple.git']]])
        if(env.CUSTOM_TAG != '')
		  {
		  def tt = sh (returnStatus: true, script: '''
          gittag=`git tag -l $CUSTOM_TAG`

            if [[ -n "$gittag"  ]]; then
                    exit 1
            else
                    exit 0
            fi''')
	
		  echo "${tt}"
	
		  }
      }
}
