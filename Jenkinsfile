pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID='f6326460-6e70-428f-8e68-21644fb59d12'
    }

    stages {
        stage('nested stages'){

            parallel{
                stage('Deploy') {
                        agent{
                            docker{
                                image 'node:18-alpine'
                                reuseNode true
                            }
                        }
                        steps {
                            sh '''
                                npm install netlify-cli
                                node_modules/.bin/netlify --version
                                echo "Deploying to production Site ID: $NETLIFY_SITE_ID

                            '''
                        }
                        post{
                        always{
                            cleanWs()
                        }
                    }
                }
            }         
        }
    } 
}

