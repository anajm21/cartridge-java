Jenkinsfile (Declarative Pipeline)
pipeline {
    agent { docker 'maven:3.3.3' }

    stages {
        stage('Build & Package') {
            steps {
                git 'https://github.com/Accenture/spring-petclinic.git'
				environment {
					workspaceFolderName = 'WORKSPACE_NAME'
					projectFolderName = 'PROJECT_NAME'
				}
				step([$class: 'CopyArtifact', fingerprintArtifacts: true, parameters: 'ADOP MAVEN', projectName: 'clean install -DskipTests'])


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