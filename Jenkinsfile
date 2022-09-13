pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                sh 'printenv' 
                echo "${WORKSPACE}/Builds/${env.JOB_NAME}-${env.BUILD_NUMBER}"
                echo "SCM Trigger test done!!"
                slackSend color: '#BADA55', message: 'Hello, World!'
               
                                     
            }
        }
	
	stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-1',credentials:'airflowcred') {
                  sh 'echo "Upload to S3 bucket"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, bucket:'airflowtest-dag')
                  }
              }
         }

    }
}
