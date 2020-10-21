node{

		stage('CheckOut'){
			steps{
				checkout([$class: 'TeamFoundationServerScm',credentialsConfigurer: [$class: 'AutomaticCredentialsConfigurer'], projectPath: '$/ILESB_Onprem/SourceCode/ILServices-UAT/ESB', serverUrl: 'http://iltfs/tfs/ilprojectcollection02', useOverwrite: true,useUpdate: true,workspaceName: 'Hudson-${JOB_NAME}-${NODE_NAME}',versionSpec :"${params.versionSpec}"])
          			}
			}
    	stage('Restore'){
		    steps{
			    bat "dotnet restore"
		    }}
    	stage('Clean'){
		    steps{
        		bat "dotnet clean ESB.sln"
        	}}
        
		stage('Build'){
	    	steps{
			    bat "dotnet build --configuration Release ESB.sln"
    }}


}
