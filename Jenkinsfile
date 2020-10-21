node{

	stage('CheckOut'){
		checkout([$class: 'TeamFoundationServerScm',credentialsConfigurer: [$class: 'AutomaticCredentialsConfigurer'], projectPath: '$/ILESB_Onprem/SourceCode/ILServices-UAT/ESB', serverUrl: 'http://iltfs/tfs/ilprojectcollection02', useOverwrite: true,useUpdate: true,workspaceName: 'Hudson-${JOB_NAME}-${NODE_NAME}'])
          	}
    	stage('Restore'){
		bat "dotnet restore"
		}
    	stage('Clean'){
		bat "dotnet clean ESB.sln"
        	}
	stage('Build'){
		bat "dotnet build --configuration Release ESB.sln"
    }
}
