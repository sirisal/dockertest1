pipeline {
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
                    sh 'sudo docker build -t 0807as/somu:$BUILD_NUMBER .'
                }
            }
            stage('Restart the NGINX Sever') {
                steps {
                    sh 'sudo systemctl restart nginx'
                    sh 'sudo systemctl status nginx'
                }
            }
            stage('Verifying The Deployment') {
                steps {
                    sh 'ls /var/www/html/'
                }
            }
    }
}
