pipeline{
    agent{
        label "master-1"
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

    }
}