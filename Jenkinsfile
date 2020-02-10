
    pipeline {
        agent {
            any
        }
        parameters {
             booleanParam(name: 'RUN_CLOUDFORMATION', defaultValue: false, description: 'Run the cloudformation stack') 
        }
        environment {
            env = 'DEV'
        }
        stages {

            stage('test') { 
                steps { 
                    echo "test"
                }
            }
            stage('Run cloudformation') {
                when {
                    expression { params.RUN_CLOUDFORMATION == true}
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