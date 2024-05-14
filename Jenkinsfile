pipeline{
	agent{ label 'Jenkins-Agent'}
	tools {
		jdk 'Java17'
		maven 'Maven 1'
	}
	stages{
		stage("Cleanup Workspace"){
			steps{
				cleanWs()
			}
		}
		stage("Checkout from SCM"){
			steps{
				git branch: 'main', credentialsId: 'github', url: 'https://github.com/deepakrk0520/accounts'
			}
		}
		stage("Build Application1"){
			steps{
				sh "mvn clean package"
			}
		}
		stage("Build Application"){
			steps{
				sh "mvn clean package"
			}
		}
		stage("Test Application"){
			steps{
				sh "mvn test"
			}
		}
	}
}
