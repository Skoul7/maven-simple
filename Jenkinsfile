node 
{
    stage('Checkout')
      {
        checkout([$class: 'GitSCM', branches: [[name: '${TAG}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Sahil_Koul_github', url: 'https://github.com/Skoul7/maven-simple.git']]])
        if(env.CUSTOM_TAG != '')
		  {
		  def tag = sh (script: '''
                  gitTag=`git tag -l $CUSTOM_TAG`

               if [[ -n "$gitTag"  ]]; then
                      exit 1
               else
                      exit 0
               fi''')
	
		  echo "${tag}"
		  if( tag == 1 )
		  {
		 	 currentBuild.result = 'ABORTED'
          		 error('Tag version is already occupied. Please use another version')
		  
		  }
		  }
      }
}
