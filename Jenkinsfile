pipeline {
    agent {
        label 'node-1'
    }
    triggers {
        cron('H * * * 1-5')
        pollSCM('* * * * *')
    }
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'enter the mavengoal')
    }
    stages {
        stage('scm'){
            steps{
                git "url"
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
}