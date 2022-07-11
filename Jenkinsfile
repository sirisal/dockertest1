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
                    script { 
                       sudo docker.withRegistry( '',registryCredential ) {
                            dockerImage.push("$BUILD_NUMBER")
                            dockerImage.push('latest')
            } 
                }
            }
            }
    }
}
