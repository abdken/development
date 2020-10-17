pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Lint HTML') {
            steps {
                sh 'tidy -q -e *.html'
            }
        }
        // aquaMicroscanner token is missing / no emails sent!
        // stage('Security Scan') {
        //     steps { 
        //         aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 4', onDisallowed: 'fail', outputFormat: 'html'
        //     }
        // }         
        stage('Upload to AWS') {
            steps {
                withAWS(region:'ca-central-1',credentials:'default') {
                sh 'echo "Uploading content with AWS creds"'
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-devops-pipeline')
                }
            }
        }
    }
}
