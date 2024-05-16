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
            DOCKER_REGISTRY = 'https://index.docker.org'
	    
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
		
		stage("Build & Push Docker Image") {
    			steps {
      				script {
        				withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          					docker.withRegistry(DOCKER_REGISTRY, DOCKER_PASS) { // Use retrieved credentials
            						docker_image = docker.build "${IMAGE_NAME}"  // Build the image
            						docker_image.push("${DOCKER_REGISTRY}/${IMAGE_NAME}") // Push using image name with registry
          					}
        				}
      				}
    			}
  		}
	}
}
