pipeline{
	agent any
	tools {
		'org.jenkinsci.plugins.docker.commons.tools.DockerTool' 'docker2'
	}	
	stages {
		stage('Clone repository') {
			/* Let's make sure we have the repository cloned to our workspace */
			steps {
				checkout scm
				sh "docker version" 
			}
		}
		stage('maven install') {
			steps {
			  withMaven( maven: 'Maven3') {
					sh 'mvn -f ./BinaryCalculatorWebapp/ clean package'
				}
			}
		}
		stage('Create Docker image') {
			steps{
				script{
					app=docker.build("CalculatorWebapp", "./BinaryCalculatorWebapp")
				}	
			}
		}
	}
}