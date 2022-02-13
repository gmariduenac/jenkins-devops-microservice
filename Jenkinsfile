//SCRIPTED WAY
/*node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
	stage('Integration Test') {
		echo "Test"
	}
}*/
//DECLARATIVE WAY
pipeline {
	agent any
	stages{
		stage('Build'){
			steps{
				echo "Build"
			}	
		}
		stage('Test'){
			steps{
				echo "Test"
			}	
		}
		stage('Integration Test'){
			steps{
				echo "Integration Test"
			}	
		}				
	} post {
		always{
			echo "I am awesome, I run always"
		}
		success{
			echo "I run when you are successfull"
		}
		failure{
			echo "I run when you fail"
		}
	}
}