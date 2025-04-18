pipeline {
    agent any

    stages {
        parallel{

            stage('Build') {
                        agent{
                            docker{
                                image 'node:18-alpine'
                                reuseNode true
                            }
                        }
                        steps {
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
                    post{
                        always{
                            cleanWs()
                        }
                    }
                }
                    

            stage ('task parll 2'){
                sh 'echo parallel2'
            }

            stage('task parll 3'){
                sh 'echo parallel3'
            }
        
    }
}
