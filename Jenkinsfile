pipeline {

    environment {
     registryCredential = 'dockercred'   
    }
    agent {
         label 'docker'
    }

    stages {
        stage ('Prompt for input') {
            steps {
                script {
                    env.string = input message: 'Please choose your option',
                             parameters: [string(defaultValue: 'Ready to go?',
                                          description: '',
                                          name: '')]
                }
            }
        }
            stage('Cloning our Git') {
                steps {
                    git 'https://github.com/somu1679/dockertest1.git'
                }
            }
            stage('Build an image using docker file') {
                steps {
                    sh 'sudo docker build -t 0807as/somu:v$BUILD_NUMBER .'
                }
            }
            stage('Push an image to docker hub') {
                steps {
                withCredentials([string(credentialsId: 'cred', variable: 'docker')]) {
                sh "docker login -u 0807as -p ${docker}"
                sh "docker push 0807as/somu:v$BUILD_NUMBER"
            }    
            } 
            }            
            }
    }
}
