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
	//agent any
	agent { docker { image 'maven:3.6.3' }}
	/*environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "dockerHome/bin:mavenHome/bin:$PATH"
	}*/
	stages {
		stage('Build'){
			steps{
				sh "mvn --version"
				//sh "docker version"
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
	} 
	post {
		always{
			echo "I am awesome, I run always"
		}
		success{
			echo "I run when you are successfull"
		}
		failure{
			echo "I run when you fail"
		}
		changed{
			echo "I run when you status changed from one execution to another"
		}
	}
}