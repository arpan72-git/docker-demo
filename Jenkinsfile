pipeline{
	agent any
	
	stages{
		stage('Clean'){
			
			steps{
				echo "Cleaning project"
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
		
		stage('Docker Build'){
			steps{
				echo "Docker build"
				//withMaven(maven: 'maven_3_6_3'){
				//	bat 'mvn deploy'
				//}
			}
		}
		
		stage('Docker Deploy'){
			
			steps{
				echo "Deploying to docker"
				//withMaven(maven: 'maven_3_6_3'){
				//	bat 'mvn clean compile'
				//}
			}
		}
		
	}

}
