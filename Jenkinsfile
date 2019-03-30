#!/usr/bin/env groovy

@Library('jenkins-global-libraries') _

def githubToken = '8ad35613-0fb3-4b54-ba54-a65da52fca53'
def pom

pipeline {
	agent { label 'docker-maven-slave' }
	stages {
		stage('Build') {
			steps {
				glMavenBuild skipTest: true
			}
		}
//        stage('Quality Scan') {
//            echo "Placeholder for Sonar scans"
//        }
		stage('Publish to Nexus') {
            when { branch 'master' }
			steps {
				glPublishToNexus credentialsId: "${githubToken}",
					skipTest: true,
					settingsXml: "mavenSettings.xml"
			}
		}
	}
}
