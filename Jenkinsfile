pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID='f6326460-6e70-428f-8e68-21644fb59d12'
        NETLIFY_AUTH_TOKEN=credentials('netlify-token')
        NPM_CONFIG_LOGLEVEL='error'
        REACT_APP_VERSION="1.0.$BUILD_ID"
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
                cleanWs()
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }

        }
        stage('Deployments'){

            parallel{

                stage('Deploy Staging') {
                        agent{
                            docker{
                                image 'node:18-alpine'
                                reuseNode true
                            }
                        }
                        steps {
                            sh '''
                                echo "Deploying to staging Site ID: $NETLIFY_SITE_ID"
                                node_modules/.bin/netlify status
                                node_modules/.bin/netlify deploy --dir=build

                            '''
                        
                        }
                }
                stage('Deploy Prod') {
                        agent{
                            docker{
                                image 'node:18-alpine'
                                reuseNode true
                            }
                        }
                        steps {
                            sh '''
                                echo "Deploying to production Site ID: $NETLIFY_SITE_ID"
                                node_modules/.bin/netlify status
                                node_modules/.bin/netlify deploy --dir=build --prod

                            '''
                        }
                    }
                }
            }         
        }
    } 


