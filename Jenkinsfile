node{
	try{
	
	notifyStarted()

	stage('CheckOut'){
		checkout([$class: 'TeamFoundationServerScm',credentialsConfigurer: [$class: 'AutomaticCredentialsConfigurer'], projectPath: '$/ILESB_Onprem/SourceCode/ILServices-UAT/ESB', serverUrl: 'http://iltfs/tfs/ilprojectcollection02', useOverwrite: true,useUpdate: true,workspaceName: 'Hudson-${JOB_NAME}-${NODE_NAME}', versionSpec :"${params.versionSpec}"])
          	}
    	stage('Restore'){
		bat "dotnet restore"
		}
    	stage('Clean'){
		bat "dotnet clean ${params.solution}"
        	}
	stage('Build'){
		bat "dotnet build --configuration Release ${params.solution}"
		}
	stage('Publish'){
		def now = new Date()
        	bat "dotnet publish ${params.PublishProj} -o ${params.Folder}//${JOB_NAME}//${now.format("yyyy-MM-dd")}//${BUILD_ID}"
	}
	
	notifySuccessful()
	} catch (e) {
    currentBuild.result = "FAILED"
    notifyFailed()
    throw e
  }
}
def notifyStarted() {
  // send to email
emailext( 
	attachmentsPattern: 'test/myPdf3*', body: '''<p>STARTED: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\':</p>
<p>Check console output at &QUOT;<a href=\'${env.BUILD_URL}\'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>''', 
	compressLog: true, 
	mimeType: 'text/html', 
	recipientProviders: [buildUser()], 
	replyTo: 'sunny9402.ss@gmail.com', 
	subject: 'STARTED: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\'', 
	to: 'sunny9402.ss@gmail.com'
	)
}

def notifySuccessful() {
  emailext (
      to: '1018341@icicilombard.com',
      subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
      recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )
}

def notifyFailed() {
  emailext (
      to: '1018341@icicilombard.com',
      subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
      recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )
}

