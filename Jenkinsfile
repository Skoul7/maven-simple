node 
{
    stage('Checkout')
      {
        checkout([$class: 'GitSCM', branches: [[name: '${TAG}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Sahil_Koul_github', url: 'https://github.com/Skoul7/maven-simple.git']]])
        if(env.CUSTOM_TAG != '')
		  {
		  sh '''
		  gitTagExists=`git tag -l $CUSTOM TAG`
		  '''
			  if(env.gitTagExists != '')
			  {
		           currentBuild.result = 'ABORTED'
                           error('Tag version is already occupied. Please use another version')	
		          }
		  }
      }
}
