#!/usr/bin/env groovy

pipeline {
    agent any
    triggers {
        pollSCM "H/1 * * * *"
        //cron "* * * * * % BUILD_TYPE=rc"
        parameterizedCron('''
        */2 * * * * % BUILD_TYPE=nightly
        ''')
    }
    parameters {
            choice(
                name: 'BUILD_TYPE',
                choices:"Nightly\nSnapshot\nRelease",
                description: "Nightly for internalodd releases - 4.1, 4.3, 4.5...! \n Release for customer/even releases - 4.0, 4.2, 4.4....")
            
            //choice(name:'BUILD_TYPE',choices:['Nightly','Snapshot','Release'], description:'Nightly for internalodd releases - 4.1, 4.3, 4.5...! \n Release for customer/even releases - 4.0, 4.2, 4.4..')
            string(name: 'BRANCH_TO_BE_BUILT', defaultValue: '${SE_DEFAULT_BRANCH}', description: 'Specify the branch from which you want to create the build P.S. - Make sure all the required repositories for this build has this branch. Otherwise the build will fail. default branch is current release no need to change untill you want to build different release')
            string(name: 'UI_VERSION', defaultValue: '${SE_DEFAULT_BRANCH}')
            booleanParam(name: 'FULL_BUILD', defaultValue: false)
            booleanParam(name: 'PATCH_BUILD', defaultValue: true)
            choice(name: 'WLS_VERSION', choices: ['12.2.1.2.0', '12.1.3'], description: 'WLS Client Version')
            
            
    }
    stages {
        stage("build") {
            steps {
                //echo "Working"
                sh 'env'
                echo "Hello ${params.BUILD_TYPE}"
                echo "Global ${SE_DEFAULT_BRANCH}"
            }
        }
        
        stage('stage1') {
  steps {
    wrap([$class: 'BuildUser']) {
      echo "${BUILD_USER}"
      echo "${BUILD_USER_ID}"
      echo "${BUILD_USER_EMAIL}"
    }
}
}
        
        stage('get user name') {
            steps {
              // echo "${BUILD_USER_ID}" 
                sh 'pwd'
            }
        }
        
        
    }
    
}
   
