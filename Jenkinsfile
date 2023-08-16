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
         stage('PrepareFile') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                      fallocate -l 5342880000 test.zip 
                 '''
             }
         }  
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-1',credentials:'ec2-user') {
                  sh 'echo "Uploading content with AWS creds"'
                      // s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'app.py', bucket:'jenkins-s3-bucket-softrams-test')
                       aws s3 cp test.zip s3://jenkins-s3-bucket-softrams-test/
                  }
              }
         }
     }
}
