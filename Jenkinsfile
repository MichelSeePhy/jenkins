pipeline {
    agent any

    environment{
        // NETLIFY_AUTH_TOKEN = credentials('netlify-auth-token')
        NETLIFY_SITE_ID = '63c04e0e-0fc1-4448-8dd4-b57db1d2335c'
    }

    stages {
     stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        // stage('Run tests') {
        //     parallel {
        //         stage('Unit Tests') {
        //             agent {
        //                 docker {
        //                     image 'node:18-alpine'
        //                     reuseNode true
        //                 }
        //             }
        //             steps {
        //                 sh '''
        //                     test -f build/index.html
        //                     npm test
        //                 '''
        //             }
        //             post {
        //                 always {
        //                     junit 'jest-results/junit.xml'
        //                 }
        //             }
        //         }
        //         stage('E2E') {
        //             agent {
        //                 docker {
        //                     image 'mcr.microsoft.com/playwright:v1.55.1-jammy'
        //                     reuseNode true
        //                 }
        //             }
        //             steps {
        //                 sh '''
        //                     npm install serve
        //                     node_modules/.bin/serve -s build &
        //                     sleep 10
        //                     npx playwright test --reporter=html
        //                 '''
        //             }
        //              post {
        //                 always {
        //                     publishHTML([
        //                         allowMissing: false,
        //                         alwaysLinkToLastBuild: false,
        //                         icon: '',
        //                         keepAll: false,
        //                         reportDir: 'playwright-report',
        //                         reportFiles: 'index.html',
        //                         reportName: 'Playwright HTML Report',
        //                         reportTitles: '',
        //                         useWrapperFileDirectly: true
        //                     ])
        //                 }
        //             }
        //         }
        //     }
        // }

          stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install netlify-cli@20.1.1
                node_modules/.bin/netlify --version
                echo "Deploying to PRODUCTION. Site id: $NETLIFY_SITE_ID"
                '''
            }
        }
    }

}
