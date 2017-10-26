pipeline {
    agent {label 'swarm'}
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
				sh "./mvnw clean install -DskipTests"		
            }
        }
        stage('Unit & Mutation Test') {
            steps {
				//sh "./mvnw surefire:test"
				sh 'echo hola'
            }
        }
        stage('Code Inspection') {
            steps {
                withSonarQubeEnv('sonar_ana') {
					//sh './mvnw sonar:sonar'
					sh 'echo hola'
    
				}

            }
        }
		stage('Provision & Deploy to Test') {
		
			
            steps {
			        
					sh ''' 
					docker cp target/petclinic.war tomcat:/usr/local/tomcat/webapps/
					docker restart tomcat
					COUNT=1
					while ! curl -q http://34.251.50.161:8888/petclinic -o /dev/null
					do
					  if [ ${COUNT} -gt 10 ]; then
						echo "Docker build failed even after ${COUNT}. Please investigate."
						exit 1
					  fi
					  echo "Application is not up yet. Retrying ..Attempt (${COUNT})"
					  sleep 5
					  COUNT=$((COUNT+1))
					  done
					echo "=.=.=.=.=.=.=.=.=.=.=.=."
					echo "=.=.=.=.=.=.=.=.=.=.=.=."
					echo "Environment URL (replace PUBLIC_IP with your public ip address where you access jenkins from) : http://34.251.50.161:8888/petclinic"
					echo "=.=.=.=.=.=.=.=.=.=.=.=."
					echo "=.=.=.=.=.=.=.=.=.=.=.=."
					'''
            }
        }
		stage('InTegration & Security Test') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'adop-cartridge-java-regression-tests']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Accenture/adop-cartridge-java-regression-tests.git']]])
				sh "./mvnw -f regression-tests/pom.xml clean -B test -DPETCLINIC_URL=http://172.17.0.1:8080/petclinic -DZAP_ENABLED="false""
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