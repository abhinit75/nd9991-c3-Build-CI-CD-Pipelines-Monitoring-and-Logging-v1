pipeline {
     agent any
     environment {
        AWS_ACCESS_KEY_ID     = credentials('AKIA2ZKMI5RIROCOOP6M')
        AWS_SECRET_ACCESS_KEY = credentials('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')
    }
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
         stage('Security Scan') {
              steps { 
                 aquaMicroscanner imageName: 'alpine:latest', notCompleted: 'exit 1', onDisallowed: 'fail'
              }
         }         
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-west-2',credentials:'JenkinsAccess') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'jenkinsbucketabhi', path:'/Users/abhi/Desktop/Jenkins Demo/nd9991-c3-Build-CI-CD-Pipelines-Monitoring-and-Logging-v1/index.html')
                  }
              }
         }
     }
}
