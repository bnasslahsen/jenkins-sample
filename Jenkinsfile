// Powered by Infostretch 

timestamps {

node () {

	stage ('App-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/bnasslahsen/jenkins-sample.git']]]) 
	}
	stage ('App-IC - Build') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean package " 
			} else { 
 				bat "mvn clean package " 
			} 
 	}
}

	stage ('App-IC - Build') {
		withSonarQubeEnv('sonar') {
			bat 'mvn sonar:sonar'
		}
	}
	
}
}
