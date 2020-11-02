node{

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
	stage('Publish'){
		def now = new Date()
        	bat "dotnet publish ${params.PublishProj} -o ${params.Folder}//${JOB_NAME}//${now.format("yyyy-MM-dd")}//${BUILD_ID}"
	}
		stage('Email'){
			always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
			}}
    }
}
