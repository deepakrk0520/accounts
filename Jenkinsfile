pipeline{
	agent{ label 'Jenkins-Agent'}
	tools {
		jdk 'Java17'
		maven 'Maven 1'
	}
	environment {
	    APP_NAME = "accounts"
            RELEASE = "1.0.0"
            DOCKER_USER = "deepakrk0520"
            DOCKER_PASS = 'dockerhub'
            IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
            IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
	    
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
		stage("Compile") {
    			steps {
	    			def pomProjectVersion = sh script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout', returnStdout: true
    			}
		}
		stage("Build & Push Docker Image") {
            		steps {
                		script {
                    			docker.withRegistry('',DOCKER_PASS) {
                        			docker_image = docker.build "${IMAGE_NAME}"
                    			}

                    			docker.withRegistry('',DOCKER_PASS) {
                        
			    		docker_image.push(docker.io/jaanvideepak/dockerhub)
			    		docker_image.push('latest')
                    			}
                		}
            		}

       		}
	}
}
