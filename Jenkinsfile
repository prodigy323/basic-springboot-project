#!/usr/bin/env groovy

def githubToken = '8ad35613-0fb3-4b54-ba54-a65da52fca53'

pipeline {
	agent { label 'docker-maven-slave' }
	stages {
		stage('Build') {
			steps {
				sh "mvn -B -Dskiptests=true clean install"
			}
		}
		stage('Publish to Nexus') {
			steps {
				def pomVersion = readMavenPom().getVersion()
				withCredentials([string(credentialsId: "${githubToken}", variable: 'TOKEN')]) {
					sh """
						mvn -B -s mavenSettings.xml deploy
						git config user.email "jhng323@gmail.com"
						git config user.name "prodigy323"
						git tag -am "${pomVersion}"
						git push --tags https://\${TOKEN}@github.com/prodigy323/basic-springboot-project.git
					"""
				}
			}
		}
		stage('Bump Version') {
			steps {
				withCredentials([string(credentialsId: "${githubToken}", variable: 'TOKEN')]) {
					sh '''
						#mvn build-helper:parse-version versions:set -DnewVersion='\${parsedVersions.majorVersion}.\${parsedVersion.MinorVersion}.\${parsedVersion.NextIncrementalVersion}-SNAPSHOT'
						mvn -B versions:set -DnextSnapshot
						git config user.email "jhng323@gmail.com"
						git config user.name "prodigy323"
						git commit -am "[ci skip] Bump Snapshot Version"
						git push https://${TOKEN}@github.com/prodigy323/basic-springboot-project.git
					'''
				}
			}
		}
	}
}
