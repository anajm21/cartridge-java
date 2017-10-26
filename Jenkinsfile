pipeline {
    agent {label 'swarm'}
	environment {
        WORKSPACE_NAME = 'ana'
        PROJECT_NAME = 'projectFolderName'
        PROJECT_NAME_KEY = 'projectNameKey'
		
    }

	tools {
		maven 'M3'
		ant 'AntApache'
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
			        
					/*sh ''' 
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
					'''*/
					sh 'echo hola'
            }
        }
		stage('InTegration & Security Test') {
            steps {
                //checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'adop-cartridge-java-regression-tests']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Accenture/adop-cartridge-java-regression-tests.git']]])
     			//sh "mvn -f adop-cartridge-java-regression-tests/pom.xml clean -B test -DPETCLINIC_URL=http://34.251.50.161:8888/petclinic -DZAP_ENABLED='false'"
				sh 'echo hola'
            }
        }
		stage('Performance Test') {
            steps {
                sh '''
				if [ ! -e apache-jmeter-2.13.tgz ]; then
					wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-2.13.tgz
				fi
				tar -xf apache-jmeter-2.13.tgz
				echo 'Changing user defined parameters for jmx file'
				sed -i 's/PETCLINIC_HOST_VALUE/34.251.50.161/g' src/test/jmeter/petclinic_test_plan.jmx
				sed -i 's/PETCLINIC_PORT_VALUE/8888/g' src/test/jmeter/petclinic_test_plan.jmx
				sed -i 's/CONTEXT_WEB_VALUE/petclinic/g' src/test/jmeter/petclinic_test_plan.jmx
				sed -i 's/HTTPSampler.path"></HTTPSampler.path">petclinic</g' src/test/jmeter/petclinic_test_plan.jmx
            	
				ant -buildfile apache-jmeter-2.13/extras/build.xml -Dtestpath=${WORKSPACE}/src/test/jmeter -Dtest=petclinic_test_plan
				
				sed -i "s/###TOKEN_VALID_URL###/http:\\/\\/34.251.50.161:8888/g" ${WORKSPACE}/src/test/gatling/src/test/scala/default/RecordedSimulation.scala
				sed -i "s/###TOKEN_RESPONSE_TIME###/10000/g" ${WORKSPACE}/src/test/gatling/src/test/scala/default/RecordedSimulation.scala
				
				mvn -f src/test/gatling/pom.xml gatling:execute
    	
				'''
				publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '${WORKSPACE}/src/test/jmeter/', reportFiles: 'petclinic_test_plan.html', reportName: 'Jmeter Report', reportTitles: ''])

            }
			
			
        }
		stage('Provision & Deploy to Prod') {
            steps {
                echo 'Deploying....'
            }
        }
		
		
    }
}