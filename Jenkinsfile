#!/usr/bin/env groovy

pipeline {
    agent any
    triggers {
        pollSCM "H/5 * * * *"
        cron '* * * * * %BUILD_TYPE=rc'
    }
    parameters {
        choice(
        name: "BUILD_TYPE",
        choices: ["snapshot", "rc"],
        description: "Build Type")
    }
    stages {
        stage("Create Compile File in Tmp dir") {
            steps {
                sh "touch /tmp/compile.txt"
                sh "touch /tmp/compile-2.txt"
                sh "echo ${BUILD_TYPE}"
            }    
        }    
        
    }
}    
   
