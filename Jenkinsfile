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
			echo "running tests"
			steps{
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn test'
				}
			}
		}
		
		stage('Deploy'){
			echo "deploying project"
			steps{
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn deploy'
				}
			}
		}
	}

}
