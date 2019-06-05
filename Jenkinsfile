pipeline {
    agent any
    stages {
	  stage('DotNetApi') {
		steps {
			echo 'DotNetApi'
		}
	  }
	  
	  stage('Checkout') {
		steps {
			git credentialsId: 'admin', url: 'https://github.com/filipemot/DotNetCore_Web_API_Jenkins_Azure', branch: 'master'
		}
	  }
	  
	    stage('Restore PACKAGES') {
			steps {
				sh(script:"dotnet restore",returnStdout:false)
			}
		}
		
		stage('Clean') {
			steps {
				sh(script:"dotnet clean",returnStdout:false)
			}
		}
		
		stage('build and publish') {
			steps {
				sh(script: "dotnet publish --configuration Release ", returnStdout: true)
			}
		}
		
		stage('deploy') {
			steps {
					sh(script: "azureWebAppPublish azureCredentialsId: params.azure_cred_id,
						resourceGroup: params.res_group, appName: params.customersapiapp, sourceDirectory: "src/CustomersAPI/bin/Release/netcoreapp2.1/publish/"", returnStdout: true)
			}
		}
    }
}