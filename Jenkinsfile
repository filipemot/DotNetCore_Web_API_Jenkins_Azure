#!/usr/bin/env groovy

def buildTimestamp() {
    def date = new Date()
    def formattedDate = date.format('yyyyMMddHHmmss')
    return formattedDate
}
node {
        def dockerTag = buildTimestamp()
		def dockerImage = "filipemot/app";
		def pub = "bin/Release/netcoreapp2.2/publish/";
	

	  stage('DotNetApi') {

			echo 'DotNetApi'

	  }
	  

	  
		  stage('Checkout') {

				git credentialsId: 'admin', url: 'https://github.com/filipemot/DotNetCore_Web_API_Jenkins_Azure', branch: 'master'
			
		  }
		  
		stage('Restore PACKAGES') {

				sh(script:"dotnet restore",returnStdout:false)
			
		}
		
		stage('Clean') {

				sh(script:"dotnet clean",returnStdout:false)
			
		}
		
		stage('build and publish') {

				sh(script: "dotnet publish --configuration Release ", returnStdout: true)
			
		}
		
    

		stage('build docker') {

			docker.build('filipemot/jenkins_dotnet_core', '.') ;
		
			
		}
	
	
}