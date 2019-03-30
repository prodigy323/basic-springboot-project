#!/usr/bin/env groovy

@Library('jenkins-global-libraries') _

def githubToken = '8ad35613-0fb3-4b54-ba54-a65da52fca53'
def pom

pipeline {
	agent { label 'docker-maven-slave' }
	stages {
		stage('Build') {
			steps {
				glMavenBuild()
			}
		}
//		stage('Publish to Nexus') {
//			steps {
//			    script {
//			        pom = readMavenPom file: 'pom.xml'
//			    }
//				withCredentials([string(credentialsId: "${githubToken}", variable: 'TOKEN')]) {
//					sh """
//						mvn -B -DskipTests=true -s mavenSettings.xml deploy
//						git config user.email "jhng323@gmail.com"
//						git config user.name "prodigy323"
//						git tag -a ${pom.version} -m 'create tag ${pom.version}'
//						git push --tags https://\${TOKEN}@github.com/prodigy323/basic-springboot-project.git
//					"""
//				}
//			}
//		}
//		stage('Bump Version') {
//			steps {
//				withCredentials([string(credentialsId: "${githubToken}", variable: 'TOKEN')]) {
//					sh '''
//						#mvn build-helper:parse-version versions:set -DnewVersion='\${parsedVersions.majorVersion}.\${parsedVersion.MinorVersion}.\${parsedVersion.NextIncrementalVersion}-SNAPSHOT'
//						mvn -B -DskipTests=true versions:set -DnextSnapshot
//						git config user.email "jhng323@gmail.com"
//						git config user.name "prodigy323"
//						git commit -am "[ci skip] Bump Snapshot Version"
//						git push https://${TOKEN}@github.com/prodigy323/basic-springboot-project.git
//					'''
//				}
//			}
//		}
	}
}
