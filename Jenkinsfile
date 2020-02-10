
    pipeline {
        agent any
        parameters {
             booleanParam(name: 'RUN_CLOUDFORMATION', defaultValue: false, description: 'Run the cloudformation stack')
             choice choices: ['dev', 'prod'], description: 'Environment to deploy', name: 'environment'
        }
        
        stages {
            stage('Run cloudformation') {
                when {
                    expression { params.RUN_CLOUDFORMATION == true}
                }
                environment { 
                    stackName = "my-example-lambda-${params.environment}"
                }
                steps { 
                    sh "aws cloudformation create-stack --region eu-west-1 --stack-name ${stackName} --parameters ParameterKey=Environment,ParameterValue=${env},ParameterKey=Message,ParameterValue=HelloWorld"
                }
            }

 
        }
    }