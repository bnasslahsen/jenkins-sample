// Powered by Infostretch 

timestamps {

node () {

	stage ('APP-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/bnasslahsen/jenkins-sample.git']]]) 
	}
	stage ('APP-IC - Build') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean " 
			} else { 
 				bat "mvn clean " 
			} 
 		}		// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn compile " 
			} else { 
 				bat "mvn compile " 
			} 
 		}		// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn test " 
			} else { 
 				bat "mvn test " 
			} 
 		}		// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn package -DskipTests " 
			} else { 
 				bat "mvn package -DskipTests " 
			} 
 		} 
	}
	stage ('APP-IC - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'badr.nasslahsen@gmail.com', sendToIndividuals: false])
 
	}
}
}