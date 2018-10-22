pipeline {
    agent any
triggers {
        pollSCM "H/1 * * * *"
parameterizedCron('''
        */2 * * * * % BUILD_TYPE=Nightly
        ''')
               
    }
    environment {
     variable_no = getBuildUser ()
     var = 5
      }
  stages {
    stage("Test") {
        steps{
       //     wrap([$class: 'BuildUser']) {
      //echo "${BUILD_USER}"
      //echo "${BUILD_USER_ID}"
      //echo "${BUILD_USER_EMAIL}"
      
            
      script {
      //  if ( "${BUILD_USER_ID}" == "mangesh" ){
            try {
               
                echo "${variable_no}"
              echo "Any code with error"
            } catch(err) {
              echo "Error"
            }
       // }
      }
      //
          //  }
        }
    }
  }
}
def getBuildCause(){

     wrap([$class: 'BuildUser']) {
      echo "${BUILD_USER}"
      echo "${BUILD_USER_ID}"
      echo "${BUILD_USER_EMAIL}"
    }
}
@NonCPS
def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}
