node 
{
	
    stage('Checkout')
      {
        checkout([$class: 'GitSCM', branches: [[name: '${TAG}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Sahil_Koul_github', url: 'https://github.com/Skoul7/maven-simple.git']]])
        if(env.CUSTOM_TAG != '')
		  {
		  def tag = sh (returnStatus: true, script: '''
                  gitTag=`git tag -l $CUSTOM_TAG`

		       if [[ -n "$gitTag"  ]]; then
			      exit 1
		       else
			      exit 0
		       fi''')

			  echo "${tag}"
		   if( tag == 1 )
			  {
		   sendMail()
		   currentBuild.result = 'ABORTED'
          	   error('Tag is already occupied. Please use another version')
		   
		          }
		  }
      }
	stage('Tag Push') 
	{
withCredentials([string(credentialsId: 'GIT_USERNAME', variable: 'GIT_USERNAME'), string(credentialsId: 'GIT_PASS', variable: 'GIT_PASS')])
{
    sh '''
	if [[ -n "$CUSTOM_TAG" && "$PUSH_TAG" == Yes ]]; then
	{
	git tag ${CUSTOM_TAG}
	git push https://${GIT_USERNAME}:${GIT_PASS}@github.com/Skoul7/maven-simple ${CUSTOM_TAG}
	echo "Entered tag was pushed to the repository."
	}
	else
	{
	echo "No tag to push to the remote repository"
	}
	fi
	'''
}
}
}
def sendMail() {
        def MAIL_LIST="Sahil.koul@hsc.com,Sahilraju@gmail.com"
        emailext to: "${MAIL_LIST}",
             subject: "JENKINS: $JOB_NAME - Build # $BUILD_ID - ${currentBuild.result}",
             body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
             mimeType: 'text/html'
             attachLog: true
 			}
