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
         
                stage('DeployToProduction') {
         
                    steps {
                         withCredentials([sshUserPrivateKey(
                                 credentialsId: 'jenkins.shipit',
                                 keyFileVariable: 'keyfile')] {
                                     sh '''
                                     ec2-user@54.199.248.76
                                     cmd="docker ps"
                                     ssh -i "$keyfile" -o StrictHostKeyChecking=no $ec2-user $cmd
                                     '''
                     
                            
                            
                            
                    }
                }
             }
         }   

