pipeline {
    agent any
	environment {
        WORKSPACE_NAME = 'ana'
        PROJECT_NAME = 'hola'
    }
    stages {
        stage('Build & Package') {
            steps {
                git 'https://github.com/Accenture/spring-petclinic.git'
				
				tool(
					// Maven installation declared in the Jenkins "Global Tool Configuration"
					maven: "M3",
					// Maven settings.xml file defined with the Jenkins Config File Provider Plugin
					// Maven settings and global settings can also be defined in Jenkins Global Tools Configuration
					mavenLocalRepo: '.m2/repository') {
								// Run the maven build
								sh "mvn clean install"
					}

            }
        }
        stage('Unit & Mutation Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Code Inspection') {
            steps {
                echo 'Deploying....'
            }
        }
		stage('Provision & Deploy to Test') {
            steps {
                echo 'Deploying....'
            }
        }
		stage('InTegration & Security Test') {
            steps {
                echo 'Deploying....'
            }
        }
		stage('Performance Test') {
            steps {
                echo 'Deploying....'
            }
        }
		stage('Provision & Deploy to Prod') {
            steps {
                echo 'Deploying....'
            }
        }
		
		
    }
}