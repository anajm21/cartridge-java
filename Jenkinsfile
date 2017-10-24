pipeline {
    agent any
	environment {
        WORKSPACE_NAME = 'ana'
        PROJECT_NAME = 'hola'
    }
	tools {
		maven 'M3'		
	}
    stages {
        stage('Build & Package') {
            steps {
                git 'https://github.com/Accenture/spring-petclinic.git'
				sh "mvn clean install -DskipTests"		
            }
        }
        stage('Unit & Mutation Test') {
            steps {
				sh "mvn surefire:test"
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