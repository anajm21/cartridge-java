pipeline {
    agent any
	environment {
        WORKSPACE_NAME = 'ana'
        PROJECT_NAME = 'projectFolderName'
        PROJECT_NAME_KEY = 'projectNameKey'
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
                withSonarQubeEnv('sonar_ana') {
				properties('''sonar.projectKey=PROJECT_NAME_KEY
				sonar.projectName=PROJECT_NAME
				sonar.projectVersion=6.2
				sonar.language=java
				sonar.scm.enabled=false''')
    
				}

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