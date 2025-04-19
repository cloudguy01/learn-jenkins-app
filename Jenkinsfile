pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID='f6326460-6e70-428f-8e68-21644fb59d12'
        NETLIFY_AUTH_TOKEN=credentials('netlify-token')
    }

    stages {
        stage('Build'){
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }

        }
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
                                echo "Small change"
                                npm install netlify-cli
                                node_modules/.bin/netlify --version
                                echo "Deploying to production Site ID: $NETLIFY_SITE_ID"
                                node_modules/.bin/netlify status
                                node_modules/.bin/netlify deploy --dir=build --prod

                            '''
                        }/*
                        post{
                        always{
                            cleanWs()
                        }
                    }*/
                }
            }         
        }
    } 
}

