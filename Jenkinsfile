#!/usr/bin/env groovy

@Library('jenkins-global-libraries') _

def nexusCreds = 'nexus_admin'

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
				glPublishToNexus credentialsId: "${nexusCreds}",
					skipTest: true,
					settingsXml: "mavenSettings.xml"
			}
		}
	}
}
