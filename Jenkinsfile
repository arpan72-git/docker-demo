pipeline{
	agent any
	
	stages{
		stage('Compile'){
			
			steps{
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn clean compile'
				}
			}
		}
		
		stage('Test'){
			
			steps{
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn test'
				}
			}
		}
		
		stage('Deploy'){
			
			steps{
				withMaven(maven: 'maven_3_6_3'){
					bat 'mvn deploy'
				}
			}
		}
	}

}