pipeline {
    agent any

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
                                netlify --version

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

