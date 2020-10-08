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
			agent {
                docker { image 'hello-world' }
            }
			steps{
				echo "Docker build"
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
