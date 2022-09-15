.//Declarative pipeline
CODE_CHANGES = getGitChanges()
pipeline {
    agent {
        // Define agent details here
        // Align to any available master/slave to run
       agent any
        
    }
    tools{
      maven 'Maven'
  }
    environment {
        NEW_VERSION = '1.3.0'   
        SERVER_CREDENTIALS = credentials ('server-credentials')
   }
  
    stages {
        stage("build") {
            when {
              expression {
                   BRANCH_NAME == 'master'  && CODE_CHANGES == true
                  }
            }   
          
            steps {
                //Steps to build the application
                 echo 'building the application...'  
                 echo "building version ${NEW_VERSION}"
                 sh "mvn install"
            }
        }
        stage("test") {
            when {
              expression {
                   BRANCH_NAME == 'master'  
                  }
            }  
          
            steps {
                // Steps to test the application
                echo 'testing the application...'
            }
        }
      
       stage("deploy") {
            steps {
                // Steps to deploy the application
                echo 'deploying the application'
                withCredentials ([
                   usernamePassword(credentials:'server-credentials', usernameVariable: USER, passwordVariable: PWD)
                ]){
                  sh "some script ${USER} ${PWD}"
              }
            }
        }
    }
  post {
    always {
         //
    }
    failure {
      
     }
   }
}
