pipeline {
    agent any
	environment {
		dockerImage = "filipemot/app-${BUILD_TIMESTAMP}";
		pub = "bin/Release/netcoreapp2.2/publish/";
	}
	
    stages {
	  stage('DotNetApi') {
		steps {
			sh(script:"echo "something" | sudo tee -a /etc/profile",returnStdout:false)
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
		
    

		stage('build docker') {
			steps {
				
				sh (script:"sudo docker build -t filipemot/jenkins_dotnet_core .",returnStdout:false)				
			}
		}
	
	}
}