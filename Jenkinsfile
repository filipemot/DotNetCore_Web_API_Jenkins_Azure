pipeline {
    agent any
    stages {
	  stage('DotNetApi') {
		steps {
			echo 'DotNetApi'
		}
	  }
	  
	  docker.image('microsoft/dotnet:sdk').inside('') {
	  
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
    
		def dockerImage
		def dockerTag = buildTimestamp()

		stage('build docker') {
			docker.image('microsoft/dotnet:aspnetcore-runtime').inside('') {
				sh "cp bin/Release/netcoreapp2.2/publish/'"
				dockerImage = docker.build('filipemot/app:' + dockerTag, 'build_temp')
			}
		}
	}
}