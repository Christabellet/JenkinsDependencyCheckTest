pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/Christabellet/JenkinsDependencyCheckTest'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
				//dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
				dependencyCheck additionalArguments: '''
					-o './'
					-s './'
					-f 'ALL'
                    --suppression suppression.xml
					--prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
					
				dependencyCheckPublisher pattern: 'dependency-check-report.xml'
			}
		}
	}
}	
