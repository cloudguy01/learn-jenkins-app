pipeline {
    agent any

    stages {
      stage ('Spinup AWS CLI container'){
        agent{
            docker{
                image 'amazon/aws-cli'
                args "entrypoint=''"
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
        
    


