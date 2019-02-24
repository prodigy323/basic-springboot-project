pipeline {
	agent { label 'docker-maven-slave' }
	stages {
		stage('Build') {
			steps {
				sh "mvn -B -Dskiptests=true clean install"
			}
		}	
	}
}
