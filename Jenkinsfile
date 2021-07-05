pipeline {
    agent {
        label 'node-2'
    }
    triggers {
        cron('0 * * * *')
        pollSCM('* * * * *')
    }
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'enter the mavengoal')
    }
    stages {
        stage('scm'){
            steps{
                git branch: 'tester', url: 'https://github.com/Reddy-hub-sudo/dummy-spc.git'
            }
        }
        stage('Build'){
            steps{
                sh script: " mvn ${params.MAVENGOAL"
            }
        }
        stage('post build'){
            steps{
                archiveArtifacts ' '
                junit ' '
            }
        }
    }
    post {
        always {
            sendNotifications currentBuild.result
        }
    }
}