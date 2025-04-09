pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID ='b050e8a2-1a5f-42fc-a883-670fa3b20e7d'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
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
                npm config set prefix ~/npm
                npm i netlify-cli -g
                export PATH=$PATH:~/npm/bin

                node_modules/.bin/netlify --version
                echo "Deploying to production site : $NETLIFY_SITE_ID"
                node_modules/.bin/netlify --status
                '''
            }
        }
    }
}
