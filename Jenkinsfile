pipeline {
    agent any
    stages {
	  stage('DotNetApi') {
		steps {
			echo 'DotNetApi'
		}
	  }
	  
	  docker.image('microsoft/dotnet:sdk') {
	  
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
		}
    

		stage('build docker') {
			steps {
				docker.image('microsoft/dotnet:aspnetcore-runtime') {
					dockerImage = docker.build('filipemot/app:' + buildTimestamp(), 'build_temp')
				}
			}
		}
	}
}