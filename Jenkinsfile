pipeline {
	agent {
		docker { image 'maven' }
	}
	stages {
		stage ('Checkout') {
			steps {
				git branch:'master', url: 'https://github.com/derektan1801/Vulnerable-Web-Application.git'
			}
		}
		stage('Code Quality Check via SonarQube') {
			steps {
				script {
					def scannerHome = tool 'SonarQube';
					withSonarQubeEnv() {
						sh "${tool("SonarQube")}/bin/sonar-scanner \
						-Dsonar.projectKey="OWASP" \
						-Dsonar.sources=. \
						-Dsonar.host.url="http://192.168.163.136:9000" \
						-Dsonar.login="c9344a11410bbdb0b64541a5050ce130fc1e0fe3"
						}
					}
				}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}
