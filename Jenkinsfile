pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
       stage("build") {
                steps {
                    snDevOpsStep ()
                    echo "Building" 
                    sh 'mvn -X clean install -DskipTests'
                    sleep 5
                }
       }
      stage("test") {
           steps {
               catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                  snDevOpsStep ()
                  echo "Testing"
                  sh 'mvn test'
                  sleep 3
               }
             post {
                always {
                    testng '**/target/surefire-reports/*.xml' 
                }
            }
           }
        }
    
      
      stage("deploy") {
             steps{
                  snDevOpsStep ()
                  echo "deploy in prod"
                  sleep 5
                  snDevOpsChange()              
              }
      }
      
      
  }
}
