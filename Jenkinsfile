pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/Christabellet/JenkinsDependencyCheckTest.git'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				script {
					// First DependencyCheck step
					dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'

					// Second DependencyCheck step
					dependencyCheck additionalArguments: '''
						-o './'
						-s './'
						-f 'ALL'
						--suppression suppression.xml
						--prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
				}

				// This is a separate step outside of the script block
				dependencyCheckPublisher pattern: 'dependency-check-report.xml'
			}
		}
	}
}

