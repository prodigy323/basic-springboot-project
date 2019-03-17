pipeline {
	agent { label 'docker-maven-slave' }
	stages {
		stage('Build') {
			steps {
				sh "mvn -B -Dskiptests=true clean install"
			}
		}
		stage('Artifactory') {
			steps {
				echo "Artifactory step"
			}
		}
		stage('Bump Version') {
			steps {
				sh """
					#mvn build-helper:parse-version versions:set -DnewVersion='\${parsedVersions.majorVersion}.\${parsedVersion.MinorVersion}.\${parsedVersion.NextIncrementalVersion}-SNAPSHOT'
					mvn -B versions:set -DnextSnapshot
					git config user.email "jhng323@gmail.com"
					git config user.name "prodigy323"
					git commit -am "[ci skip] Bump Snapshot Version"
					git push
				"""
			}
		}
	}
}
