pipeline {
    agent any
    stages {
	  stage('DotNetApi') {
		steps {
			echo 'DotNetApi'
		}
	  }
	  

		stage('deploy') {
			steps {
				azureWebAppPublish azureCredentialsId: params.azure_cred_id, dockerImageTag:"filipemot/app", dockerRegistryEndpoint:[credentialsId:'acr',url:'dotnetcorefilipemot'],
						resourceGroup: params.res_group, appName: params.customersapiapp, publishType: 'docker'
			}
		}
    }
}