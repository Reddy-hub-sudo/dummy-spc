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
                archiveArtifacts 'target/*.jar'
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
    post {
        always {
            mail to: 'learningthoughts.in@gmail.com', 
                subject: "Status of pipeline ${currentBuild.fullDisplayName}",
                body: "${env.BUILD_URL} has result ${currentBuild.result}"
        }
    }
}