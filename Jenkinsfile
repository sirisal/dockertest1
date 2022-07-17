pipeline {

    agent {
         label 'docker'
    }
    environment {
        CONTAINER_NAME = "sudheer"
        OLD = "(docker ps --all --quiet --filter=name="$CONTAINER_NAME")"
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
                    sh 'echo "$OLD"'
                }
            }
            stage('Push an image to docker hub') {
                steps {
                withCredentials([string(credentialsId: 'pass', variable: 'cred')]) {
                sh "docker login -u 0807as -p '$cred'"
                sh "docker push 0807as/somu:v$BUILD_NUMBER"
            }    
            } 
            } 
            // stage('Remove the Existing Containers') {
             //   steps {
              //      script {
                       
               //        if ( -n "$OLD" ) 
                //       docker stop $OLD && docker rm $OLD
                        
                 //   }  
            //    }
          // }
            stage('Run the Application') {
                steps {
                sh "docker run --rm -dit --name sudheer -p 89:80 0807as/somu:v$BUILD_NUMBER" 
                sh "docker ps"
            } 
            }       
    }
}
