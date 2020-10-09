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
        stage('Security Scan') {
            steps { 
                aquaMicroscanner imageName: 'alpine:latest', notCompleted: 'exit 1', onDisallowed: 'fail'
            }
        }
        stage('Upload to AWS') {
            steps {
                withAWS(region:'ca-central-1',credentials:'default1') {
                sh 'echo "Uploading content with AWS creds"'
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-devops-pipeline')
                }
            }
        }         
         
    }
}
