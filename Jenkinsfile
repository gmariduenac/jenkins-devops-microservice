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
	//agent { docker { image 'maven:3.6.3' }}
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout'){
			steps{
				sh "mvn --version"
				sh "docker version"
				echo "Build"
				echo "$PATH"
				echo "BUILD-NUMBER - $env.BUILD_NUMBER"
				echo "BUILD-ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD-TAG - $env.BUILD_TAG"
				echo "BUILD-URL - $env.BUILD_URL"
			}	
		}
		stage('Compile'){
			steps{
				sh "mvn clean compile"
			}	
		}
		stage('Test'){
			steps{
				//echo "Test"
				sh "mvn test"
			}	
		}
		stage('Integration Test'){
			steps{
				//echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify"
			}	
		}
		stage('Package'){
			steps{
				sh "mvn package -DskipTests"
			}	
		}
		stage('Build Docker Image'){
			steps{
				//"docker build -t gmcplus/currency_exchange_devops:$env.BUILD_TAG"
				script{
					dockerImage = docker.build("gmcplus/currency_exchange_devops:${env.BUILD_TAG}")
				}
			}	
		}
		stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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