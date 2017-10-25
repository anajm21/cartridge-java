pipeline {
    agent any
	environment {
        WORKSPACE_NAME = 'ana'
        PROJECT_NAME = 'projectFolderName'
        PROJECT_NAME_KEY = 'projectNameKey'
    }

	tools {
		maven 'M3'
		org.jenkinsci.plugins.docker.commons.tools.DockerTool 'docker'
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
					sh './mvnw sonar:sonar'
    
				}

            }
        }
		stage('Provision & Deploy to Test') {
            steps {
					sh ''' 
					export SERVICE_NAME="(echo PROJECT_NAME | tr '/' '_')_ENVIRONMENT_NAME"
					docker cp WORKSPACE/target/petclinic.war  SERVICE_NAME:/usr/local/tomcat/webapps/
					docker restart SERVICE_NAME
					COUNT=1
					while ! curl -q http://SERVICE_NAME:8080/petclinic -o /dev/null
					do
					  if [ COUNT -gt 10 ]; then
					    echo "Docker build failed even after COUNT. Please investigate."
					    exit 1
					  fi
					  echo "Application is not up yet. Retrying ..Attempt (COUNT)"
					  sleep 5
					  COUNT=COUNT+1
					done
					echo "=.=.=.=.=.=.=.=.=.=.=.=."
					echo "=.=.=.=.=.=.=.=.=.=.=.=."
					echo "Environment URL (replace PUBLIC_IP with your public ip address where you access jenkins from) : http://SERVICE_NAME.PUBLIC_IP.xip.io/petclinic"
					echo "=.=.=.=.=.=.=.=.=.=.=.=."
					echo "=.=.=.=.=.=.=.=.=.=.=.=."

					'''
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