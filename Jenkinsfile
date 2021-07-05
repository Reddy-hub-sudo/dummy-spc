pipeline{
    agent{
        label "node-1"
    }
    triggers {
        cron('H * * * 1-2')
        pollSCM('* * * * *')
    }
    stages{
        stage("scm"){
            steps{
                git branch: "developer", url: "https://github.com/Reddy-hub-sudo/dummy-spc.git"
            }
        }
        stage("mvn"){
            steps{
                sh "mvn clean package"
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