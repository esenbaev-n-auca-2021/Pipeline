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
                         input 'Deploy to Production?'
                         milestone(1)
                         withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                             script {
                               sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@$prod_ip \"docker pull nur02/my-image:${env.BUILD_NUMBER}\""
                             }
                         }
                    }    
                stage('DeployToProduction') {
                    steps {
                        input 'Deploy to Production?'
                        milestone(1)
                        echo 'Connect to the PROD server'
                        sh 'ssh ec2-user@18.181.35.172'
                        sh 'docker pull nur02/my-image'
                        sh 'docker run -d -p 8080:80 nur02/my-image'
                            
                            
                            
                    }
                }
             }
         }   
