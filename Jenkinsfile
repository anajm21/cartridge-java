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
				node ('master')
				step([$class: 'CopyArtifact', fingerprintArtifacts: true, parameters: 'ADOP MAVEN', projectName: 'clean install -DskipTests'])
				archiveArtifacts '**/*'
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