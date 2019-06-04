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
			git credentialsId: 'admin', url: 'https://github.com/filipemot/dotnetapi', branch: 'master'
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
		
		stage('Build') {
			steps {
				sh(script:"dotnet build --configuration Release",returnStdout:false)
			}
		}
		
		stage('Pack') {
			steps {
				sh(script:"dotnet pack --no-build --output nupkgs",returnStdout:false)
			}
		}
    }
}