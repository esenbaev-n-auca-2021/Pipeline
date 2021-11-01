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
         
                stage('TestingOnDev') {
                        steps {
                                echo 'Connect to the Dev server'
                                sh ' ssh -o StrictHostKeyChecking=no -tt ec2-user@54.199.248.76'
                                sh 'docker pull nur02/my-image'
                                sh 'docker run -d -p 8080:80 nur02/my-image'
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
