
    pipeline {
        agent any
        parameters {
             booleanParam(name: 'RUN_CLOUDFORMATION', defaultValue: false, description: 'Run the cloudformation stack') 
        }
        environment {
            env = 'DEV'
        }
        stages {
            stage('Run cloudformation') {
                when {
                    expression { params.RUN_CLOUDFORMATION == true}
                }
                environment { 
                    stackName = "my-example-lambda-${env}"
                }
                steps { 
                    sh "aws cloudformation create-stack --region eu-west-1 --stack-name ${stackName} --parameters ParameterKey=Environment,ParameterValue=${env},ParameterKey=Message,ParameterValue=HelloWorld"
                }
            }

 
        }
    }