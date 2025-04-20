pipeline {
    agent any

    stages {
      stage ('Spinup AWS CLI'){
        agent{
            docker{
                image 'public.ecr.aws/aws-cli/aws-cli:latest'
                args "--entrypoint=''"
            }
        }
        steps {
            withCredentials([usernamePassword(credentialsId: 's3-access', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
            sh ''' 
                aws s3 ls
            '''
            }
        }
       post{
        always{
            cleanWs()
        }
       }
      }
    }
}         
        
    


