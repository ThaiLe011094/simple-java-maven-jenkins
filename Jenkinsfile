pipeline {
	agent {
		docker {
			image 'maven:3-alpine'
			args '-v /root/.m2:/root/.m2'
			args '-u root'
		}
	}
	options {
		skipStagesAfterUnstable()
	}
	stages {
		stage('Build') {
			steps {
				sh 'whoami'
				sh 'mvn -B -DskipTests clean package'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
			post {
				always {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage('Deliver') {
			steps {
				sh 'chmod 775 ./jenkins/scripts/deliver.sh'
				sh './jenkins/scripts/deliver.sh'
			}
		}
	}
}
