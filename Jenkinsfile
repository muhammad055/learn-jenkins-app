pipeline {
    agent any

    envronment{
        NETLIFY_SITE_ID ='b050e8a2-1a5f-42fc-a883-670fa3b20e7d'
    }
    stages {
        stage('Build') {
            agent{
                docker
                {
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
        stage('Test')
        {
             agent{
                docker
                {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh'''

npm test
                '''
            }
        }

         stage('Deploy')
        {
             agent{
                docker
                {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh'''
                npm i netlify_cli
                node_modules/.bin/netlify --version
                echo "Deploying to production site : $NETLIFY_SITE_ID"
                '''
            }
        }
    }
}
