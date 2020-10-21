pipeline
{
    
    stage 'CheckOut'
        checkout([
            $class: 'TeamFoundationServerScm',
            credentialsConfigurer: [$class: 'AutomaticCredentialsConfigurer'], 
            projectPath: '$/ILESB_Onprem/SourceCode/ILServices-UAT/ESB', 
            serverUrl: 'http://iltfs/tfs/ilprojectcollection02', 
            useOverwrite: true, 
            useUpdate: true, 
            workspaceName: 'Hudson-${JOB_NAME}-${NODE_NAME}',
            versionSpec :"${params.versionSpec}"
            
            ])
            
    stage 'Restore'
        echo '######################### Restore Starts ###########################################'
        bat "dotnet restore"
      
    stage 'Clean'
        echo '########################## Clean starts ##########################################'
        bat "dotnet clean ESB.sln"
        
        
    stage 'Build'
        echo '########################### Build Strated #########################################'
        bat "dotnet build --configuration Release ESB.sln"
    

}
