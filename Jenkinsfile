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
				azureWebAppPublish azureCredentialsId: params.azure_cred_id, dockerImageTag:"filipemot/app", dockerRegistryEndpoint:[credentialsId: 'dotnetcorefilipemot', url:'dotnetcorefilipemot.azurecr.io'],
						resourceGroup: params.res_group, appName: params.customersapiapp, publishType: 'docker'
			}
		}
    }
}