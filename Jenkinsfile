pipeline {
	agent { label 'docker-maven-slave' }
	stages {
		stage('Build') {
			steps {
				sh "mvn -B -Dsurefire.testFailureIgnore=true -Dskiptests=true clean install"
			}
		}	
	}
}
