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
					sh 'mvn clean'
				}
			}
		}
		
		stage('Compile'){
			
			steps{
				echo "Compiling project"
				withMaven(maven: 'maven_3_6_3'){
					sh 'mvn compile'
				}
			}
		}
		
		stage('Unit Tests'){
			steps{
				echo "Running unit tests"
				withMaven(maven: 'maven_3_6_3'){
					sh 'mvn test'
				}
			}
		}
		
		stage('Publish'){
			steps{
				echo "Publish app"
				withMaven(maven: 'maven_3_6_3'){
					sh 'mvn package'
				}
			}
		}
		
		stage('Docker Build'){
			steps{	
				echo "Docker Build"
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
				echo "Docker Deploy"
				sh "changeTag.sh"
				withKubeConfig([credentialsId: 'mykubeconfig', serverUrl: 'https://kubernetes.docker.internal:6443']){
					bat 'kubectl apply -f nginx-deploy.yml'
					bat 'kubectl apply -f nginx-svc-np.yml'
				}
			}
		}
		
	}

}
