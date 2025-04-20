pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID='f6326460-6e70-428f-8e68-21644fb59d12'
        NETLIFY_AUTH_TOKEN=credentials('netlify-token')
        NPM_CONFIG_LOGLEVEL='error'
        REACT_APP_VERSION="1.0.$BUILD_ID"
    }

    stages {
      stage ('Build Docker image'){
        sh '''
            docker build -t my-playwright .
        '''
      }
    }
}         
        
    


