pipeline {
    agent {
        label 'node-1'
    }
    triggers {
        cron('H * * * 1-2')
        pollSCM('* * * * *')
    }
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'enter the mavengaoal')
    }
    options {
        timeout(time: 5, unit: 'MINUTES')
    }
    stages {
        stage('scm') {
            steps{
                git branch: 'qa', url: 'https://github.com/Reddy-hub-sudo/dummy-spc.git'
            }
        }
        stage('build') {
            steps{
                sh script: "mvn ${params.MAVENGOAL}"
            }
        }
        stage('post build') {
            steps{
                junit 'target/surefire-reports/*.xml'
                archiveArtifacts 'target/*.jar'
            }
        }
    }     
}