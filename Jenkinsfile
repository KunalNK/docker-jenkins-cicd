pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-jenkins-cicd')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t docker-jenkins-cicd:1.1 .'
			}
		}

		stage('Login') {

			steps {

				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
                sh 'docker tag docker-jenkins-cicd:1.1$DOCKERHUB_CREDENTIALS_USR/docker-jenkins-cicd:1.1'
				sh 'docker push $DOCKERHUB_CREDENTIALS_USR/docker-jenkins-cicd:1.1'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}