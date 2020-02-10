
    pipeline {
        agent any
        parameters {
             booleanParam(name: 'RUN_CLOUDFORMATION', defaultValue: false, description: 'Run the cloudformation stack')
             choice choices: ['dev', 'prod'], description: 'Environment to deploy', name: 'environment'
        }
        environment { 
            s3CFReleaseBucket = "jworks-cf-releases"
            cfTemplateName = "example-lambda.yaml"
        }
        stages {
            stage('Upload cloudformation') { 
                when {
                    expression { params.RUN_CLOUDFORMATION == true}
                }
                steps { 
                    sh "aws s3 cp cloudformation/${cfTemplateName} s3://${s3CFReleaseBucket}"
                }
            }
            stage('Run cloudformation') {
                when {
                    expression { params.RUN_CLOUDFORMATION == true}
                }
                environment { 
                    stackName = "my-example-lambda-${params.environment}"
                }
                steps { 
                    sh "aws cloudformation create-stack --region eu-west-1 \
                                             --stack-name ${stackName} \
                                             --parameters ParameterKey=Environment,ParameterValue=${env},ParameterKey=Message,ParameterValue=HelloWorld \
                                             --template-url https://${s3CFReleaseBucket}.s3.amazonaws.com/${cfTemplateName}"
                }
            }

 
        }
    }