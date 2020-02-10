def call( AGENT_LABEL = 'maven_jdk8' ) {
    pipeline {
        agent {
            label AGENT_LABEL
        }
        parameters {
             booleanParam(name: 'RUN_CLOUDFORMATION', defaultValue: false, description: 'Run the cloudformation stack') 
        }
        environment {
            env = 'DEV'
        }
        stages {


            stage('Run cloudformation') {
                when {
                    expression = { params.RUN_CLOUDFORMATION == true}
                }
                environment { 
                    stackName = "my-example-lambda-${env}"
                }
                steps { 
                    sh "aws cloudformation create-stack --region eu-west-1 --stack-name ${stack-name} --parameters Environment=${env},Message=Hello world"
                }
            }

 
        }
    }
}