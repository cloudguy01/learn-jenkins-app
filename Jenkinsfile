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
            cleanWs()
            sh '''
                aws --version    
            '''
        }
       
      }
    }
}         
        
    


