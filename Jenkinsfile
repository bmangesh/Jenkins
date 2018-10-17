#!/usr/bin/env groovy

pipeline {
    agent any
    triggers {
        pollSCM "H/1 * * * *"
        //cron "* * * * * % BUILD_TYPE=rc"
        parameterizedCron('''
        */2 * * * * % BUILD_TYPE=rcc
        ''')
    }
    parameters {
        choice(
        name: "BUILD_TYPE",
        choices: ["snapshot", "rcc"],
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
   
