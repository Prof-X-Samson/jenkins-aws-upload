// pipeline {
//      agent any
     
//      stages {  
//          stage('PrepareFile') {
//              steps {
//                  sh 'echo "Hello World"'
//                  sh '''
//                       fallocate -l 5342880000 test.py 
//                  '''
//              }
//          }  
//          stage('Upload to AWS') {
//               steps {
//                   withAWS(region:'us-east-1',credentials:'ec2-user') {
//                   sh 'echo "Uploading content with AWS creds"'
//                       s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'test.py', bucket:'jenkins-s3-bucket-softrams-test')
//                   }
//               }
//      }
//                 post {
//                   cleanup {
//                      echo "This block always runs after other conditions are evaluated."
//                      script {
//                          sh "rm -f ${FILE_PATH}"
//             }
//         }
//         }
//      post {
//         always {
//             cleanWs()
//             dir("${env.WORKSPACE}@tmp") {
//               deleteDir()
//             }
//             dir("${env.WORKSPACE}@script") {
//               deleteDir()
//             }
//             dir("${env.WORKSPACE}@script@tmp") {
//               deleteDir()
//             }
//         }
//     }
//      }
// }

pipeline {
    agent any
     
    stages {
        stage("Create large file") {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                      fallocate -l 5342880000 test.py 
                 '''
             }
        }
        stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-1',credentials:'ec2-user') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'test.py', bucket:'jenkins-s3-bucket-softrams-test')
                  }
              }
        }
    }
    post {
         always {
            cleanWs()
            dir("${env.WORKSPACE}@tmp") {
              deleteDir()
            }
            dir("${env.WORKSPACE}@script") {
              deleteDir()
            }
            dir("${env.WORKSPACE}@script@tmp") {
              deleteDir()
            }
        }
        }
    }
