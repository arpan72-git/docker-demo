WORKSPACE=""
pipeline{
	agent any
	
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
			agent { 
				dockerfile {
					customWorkspace '/Progra~2/Jenkins/workspace/Docker-Demo'
      					filename 'Dockerfile'
				} 
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
