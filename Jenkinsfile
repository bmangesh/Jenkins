pipeline {
    agent any
triggers {
        pollSCM "*/1 * * * *"
        //pollSCM('*/2 * * * *')
parameterizedCron('''
        */10 * * * * % BUILD_TYPE=Nightly
        ''')
               
    }
    environment {
     variable_no = getBuildUser ()
     var = 5
      }
parameters {
            choice(
                name: 'BUILD_TYPE',
                choices:"Nightly\nSnapshot\nrelease",
                description: "Nightly for internalodd releases - 4.1, 4.3, 4.5...! \n Release for customer/even releases - 4.0, 4.2, 4.4....")
            
            //choice(name:'BUILD_TYPE',choices:['Nightly','Snapshot','Release'], description:'Nightly for internalodd releases - 4.1, 4.3, 4.5...! \n Release for customer/even releases - 4.0, 4.2, 4.4..')
            string(name: 'BRANCH_TO_BE_BUILT', defaultValue: '${SE_DEFAULT_BRANCH}', description: 'Specify the branch from which you want to create the build P.S. - Make sure all the required repositories for this build has this branch. Otherwise the build will fail. default branch is current release no need to change untill you want to build different release')
            string(name: 'UI_VERSION', defaultValue: '${SE_DEFAULT_BRANCH}')
            booleanParam(name: 'FULL_BUILD', defaultValue: false)
            booleanParam(name: 'PATCH_BUILD', defaultValue: true)
            choice(name: 'WLS_VERSION', choices: ['12.2.1.2.0', '12.1.3'], description: 'WLS Client Version')
            
            
    }
  stages {
    stage("Test") {
        steps{
              //  echo "${variable_no}"
                echo "Any code with error"
        }
    }
  }
}
def getBuildCause(){

     wrap([$class: 'BuildUser']) {
         script {
            //echo "${BUILD_USER}"
            //echo "${BUILD_USER_ID}"
            //echo "${BUILD_USER_EMAIL}"
             BUILD_USER_ID = "${BUILD_USER_ID}"
         }   
    }
}
@NonCPS
def getBuildUser() {
    def causes = currentBuild.rawBuild.getCauses()
   def userCause = currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause)
    if ( userCause && env.BUILD_TYPE == "release" ) {
        wrap([$class: 'BuildUser']) {
            script {
                def BUILD_USER_ID1 = "${BUILD_USER_ID}"
            if( !( BUILD_USER_ID1 in env.AUTH_USERS ) ) 
                throw new Exception("You don't have permission to fire release Build ")
            }    
    }
    }
}

