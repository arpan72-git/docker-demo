pipeline{
	agent {
 		node {
 			label 'master'
 		}
 	}
	
	stages{
		stage('Clean'){
			
			steps{
				echo "Cleaning project"
				//dir("$WORKSPACE" ) 
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn clean'
				}
			}
		}
		
		stage('Compile'){
			
			steps{
				echo "Compiling project"
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn compile'
				}
			}
		}
		
		stage('Unit Tests'){
			steps{
				echo "Running unit tests"
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn test'
				}
			}
		}
		
		stage('Publish'){
			steps{
				echo "Publish app"
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn package'
				}
			}
		}
		
		stage('Docker Build'){
			steps{	
				script {
				    docker.withRegistry('https://registry.hub.docker.com', 'dockerHub') {

				    def customImage = docker.build("arpan62/myfirstjenkinsdockerdemo:${env.BUILD_ID}")

					/* Push the container to the custom Registry */
				    customImage.push()
				    }
				}
			}
		}
		
		stage('Docker Deploy'){
			
			steps{
				echo "Deploying to docker host"
				//withMaven(maven: 'maven_3_6_3'){
				//	sh 'mvn clean compile'
				//}
			}
		}
		
	}

}
