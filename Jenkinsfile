//scripted pipeline approach
//declarative
pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'} }
	stages {
		stage('Build') {
			steps {
				//sh "mvn --version"
				echo "Build"
				echo "$PATH"
				echo "BUILD ID - $env.BUILD_ID"
			}
		
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
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
