timestamps {

node () {

	stage ('App-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/bnasslahsen/jenkins-sample.git']]]) 
	}
	
	stage ('App-IC - Clean') {
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean" 
			} else { 
 				bat "mvn clean" 
			} 
 		}		
	}
	
	stage ('App-IC - Compile') {
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn compile" 
			} else { 
 				bat "mvn compile" 
			} 
 		}		
	}
	
	stage ('App-IC - Tests') {
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn test" 
			} else { 
 				bat "mvn test" 
			} 
 		}		
	}
	
	stage ('App-IC - Package') {
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn package -DskipTests" 
			} else { 
 				bat "mvn package -DskipTests" 
			} 
 		}		
	}
	
	stage ('App-IC - Post build actions') {
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'badr.nasslahsen@gmail.com', sendToIndividuals: false])
 
	}
}
}
