// Powered by Infostretch 

timestamps {

node () {

	stage ('APP-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/bnasslahsen/jenkins-sample.git']]]) 
	}
	stage ('APP-IC - Clean') {
 			// Maven build step

      	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn -B clean " 
			} else { 
 				bat "mvn -B clean " 
			} 
 		}
	}

	stage ('APP-IC - Compile') {
	// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn -B compile " 
			} else { 
 				bat "mvn -B compile " 
			} 
 		}
	}

	stage ('APP-IC - Test') {
	// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn -B test " 
			} else { 
 				bat "mvn -B test " 
			} 
 		}
	}

	stage ('APP-IC - Packaging') {
		// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn -B package -DskipTests " 
			} else { 
 				bat "mvn -B package -DskipTests " 
			} 
 		} 
	}
	stage('Quality check') {
	  withSonarQubeEnv('Sonar') {
		  bat "mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=jenkins-demo"
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
