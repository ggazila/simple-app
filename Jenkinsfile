pipeline {

   agent any
   triggers {
      pollSCM('H/15 * * * *')
   }
   environment {
       OKTA_OAUTH2_ISSUER           = 'https://dev-742911.okta.com/oauth2/default'
       OKTA_OAUTH2_CLIENT_ID        = credentials('OKTA_OAUTH2_CLIENT_ID')
       OKTA_OAUTH2_CLIENT_SECRET    = credentials('OKTA_OAUTH2_CLIENT_SECRET')
   }


   stages {

      stage('Build') {

         steps {

            // Get some code from a GitHub repository

            git 'https://github.com/ggazila/simple-app.git'


            // Run Maven on a Unix agent.

           // sh "./mvnw -Dmaven.test.failure.ignore=true clean package"


            // To run Maven on a Windows agent, use

             bat "mvn -Dmaven.test.failure.ignore=true clean package -s C:/Java/apache-maven-3.6.3/conf/settings.xml"

         }


         post {

            // If Maven was able to run the tests, even if some of the test

            // failed, record the test results and archive the jar file.

            success {

               junit '**/target/surefire-reports/TEST-*.xml'

               archiveArtifacts 'target/*.jar'

            }

         }

      }

   }

}
