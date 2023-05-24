pipeline {
    agent any

    environment {
        DIRECTORY_PATH = "C:/ProgramData/Jenkins/.jenkins/workspace/testngpipeline" 
        TESTING_ENVIRONMENT = "testenv" 
        PRODUCTION_ENVIRONMENT = "Prodenv"

    }
    stages {
        stage('Build-1') {
            steps {
                echo "fetch the source code from the directory path specified by the ${env.DIRECTORY_PATH}"
            }
        }
        stage('Build-2') {
            steps {
                echo "compile the code and generate any necessary artifacts" 
            }
        }
        stage('Test') {
            steps {
                echo "Unit tests" 
                echo "Integration tests" 
            }
        }
        stage('Code') {
            steps {
                echo "check the quality of the code" 
            }
        }
        stage('Deploy') {
            steps {
                echo "deploy the application to a testing environment specified by the ${env.TESTING_ENVIRONMENT}" 
            }
        }
        stage('Approval') {
            steps {
                sleep(10)
                echo "wait time is over now" 
            }
        }
        stage('Deploy to Production') {
        
            steps {
                echo "executed in this directory path: ${env.DIRECTORY_PATH}, testing envrionment of: ${env.TESTING_ENVIRONMENT}, with production envionment of: ${env.PRODUCTION_ENVIRONMENT}"
            }
            post {
                success {
                    echo "Email sent to your email address for more detail on that production"
                    
                    //  email is aligined with the pipline... . .
                    mail to: "javed.saqib94@gmail.com",
                    subject: "tesingpipline",
                    body: "executed in this directory path: ${env.DIRECTORY_PATH}, testing envrionment of: ${env.TESTING_ENVIRONMENT}, with production envionment of: ${env.PRODUCTION_ENVIRONMENT}"
                    }
                }
        }
         stage('Download') {
            steps{
               bat "del test.zip"
               zip zipFile: 'test.zip', archive: false, dir: 'directory pattern as per your structure'
            }
        }
    }
           post {
             failure {
                  emailext attachmentsPattern: 'test.zip', body: '''${SCRIPT, template="groovy-html.template"}''', 
                          subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Failed", 
                          mimeType: 'text/html',to: "email id"
            }
              success {
                  emailext attachmentsPattern: 'test.zip', body: '''${SCRIPT, template="groovy-html.template"}''', 
                        subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Successful", 
                         mimeType: 'text/html',to: "email id"
          }      
    }
    

}
