 pipeline {
    agent any

    stages {

        stage("Interactive_Input") {
            steps {
                script {
                def userInput = input(
                 id: 'userInput', message: 'Enter path of test reports:?', 
                 parameters: [
                 [$class: 'TextParameterDefinition', defaultValue: 'None', description: 'Path of config file', name: 'Config'],
                 [$class: 'TextParameterDefinition', defaultValue: 'None', description: 'Test Info file', name: 'Test']
                ])
                echo ("IQA Sheet Path: "+userInput['Config'])
                echo ("Test Info file path: "+userInput['Test'])

                }
            }
        }
    }
}
