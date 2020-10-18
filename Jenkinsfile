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
					if(isUnix()){
						sh 'mvn clean'
					}
					else{
						bat 'mvn clean'
					}
				}
			}
		}
		
		stage('Compile'){
			
			steps{
				echo "Compiling project"
				withMaven(maven: 'maven_3_6_3'){
					if(isUnix()){
						sh 'mvn compile'
					}
					else{
						bat 'mvn compile'
					}
				}
			}
		}
		
		stage('Unit Tests'){
			steps{
				echo "Running unit tests"
				withMaven(maven: 'maven_3_6_3'){
					if(isUnix()){
						sh 'mvn test'
					}
					else{
						bat 'mvn test'
					}
				}
			}
		}
		
		stage('Publish'){
			steps{
				echo "Publish app"
				withMaven(maven: 'maven_3_6_3'){
					if(isUnix()){
						sh 'mvn package'
					}
					else{
						bat 'mvn package'
					}
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
				if(isUnix()){
					sh "changeTag.sh"
				}
				withKubeConfig([credentialsId: 'mykubeconfig', serverUrl: 'https://kubernetes.docker.internal:6443']){
					if(isUnix()){
						sh 'kubectl apply -f nginx-deploy.yml'
						sh 'kubectl apply -f nginx-svc-np.yml'
					}
					else{
						bat 'kubectl apply -f nginx-deploy.yml'
						bat 'kubectl apply -f nginx-svc-np.yml'
					}
				}
			}
		}
		
	}

}
