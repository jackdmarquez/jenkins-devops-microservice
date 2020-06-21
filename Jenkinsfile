//scripted pipeline approach
//declarative
pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'} }
	environment {
		dockerHome = tool 'docker'
		mavenHome = tool 'myMaven'
		PATH="$mavenHome/bin:$dockerHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh "mvn --version"
				//sh 'docker version'
				echo "Build"
				echo "$PATH"
				echo "BUILD ID - $env.BUILD_ID"
			}
		
		}
		stage ('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
				echo "Integration Test"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
				echo "Package"
			}
		}


		stage ('Build Docker image') {
			steps {
				//"docker build -t jackod/currency-exchange:$env.BUILD_TAG"
				script {
					dockerImage= docker.build("jackod/currency-exchange:${env.BUILD_TAG}")
				}
			}

		}
		stage ('Push Docker image') {
			steps {
				script {
					docker.withRegistry('','dockerHub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}

		}

	} 
	post {
		always {
			echo "I run always"
		}
		success {
			echo "I run when successful"
		}
		failure {
			echo "I run when you fail"
		}
		//changed - it is when status changes
		
	}
	
}
