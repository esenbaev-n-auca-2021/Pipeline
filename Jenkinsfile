pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker_hub_login')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t nur02/my-image:latest .'
			}
		}

				
                stage('Login') {

                        steps {
                            sh 'docker login -p $DOCKERHUB_CREDENTIALS_PSW -u $DOCKERHUB_CREDENTIALS_USR'
                        }
                }

		stage('Push') {

			steps {
				sh 'docker push nur02/my-image:latest'
			}
		}
	}
        
        post {
            always {
                sh 'docker logout'
            }
        }

}
