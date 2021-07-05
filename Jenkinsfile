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
        timeout(time: 10, unit: 'MINUTES')
    }
    stages {
        stage('scm') {
            steps{
                git branch: 'qa', url: 'https://github.com/Reddy-hub-sudo/dummy-spc.git'
            }
        }
        stage('build') {
            steps {
                withSonarQubeEnv('SONAR-7.1') {
                    sh script: 'mvn clean package sonar:sonar'
                }

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