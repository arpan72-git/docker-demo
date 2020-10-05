pipeline{
	agent any
	
	stages{
		stage('Compile'){
			
			steps{
				echo "compiling project"
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn clean compile'
				}
			}
		}
		
		stage('Test'){
			steps{
				echo "running tests"
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn test'
				}
			}
		}
		
		stage('Deploy'){
			steps{
				echo "deploying project"
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn deploy'
				}
			}
		}
	}

}
