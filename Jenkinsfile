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
                   // mail to: "javed.saqib94@gmail.com",
                    emailext to: "javed.saqib94@gmail.com",
                    emailext attachlog: true,
                    subject: "tesingpipline",
                    body: "executed in this directory path: ${env.DIRECTORY_PATH}, testing envrionment of: ${env.TESTING_ENVIRONMENT}, with production envionment of: ${env.PRODUCTION_ENVIRONMENT}"
                    }
                }
        }
        stage('Download') {
            steps {
                  echo "artifact file" > generatedFile.txt'
             }
        }
    }
            post {
                 always {
                     archiveArtifacts artifacts: 'generatedFile.txt', onlyIfSuccessful: true
            
                     echo 'I will always say Hello again!'

                     emailext attachLog: true, attachmentsPattern: 'generatedFile.txt',
                     body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}
                     \n More info at: ${env.BUILD_URL}",
                     recipientProviders: [developers(), requestor()],
                     subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
            
                    }
        
             }
    

}
