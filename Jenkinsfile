pipeline{
    agent { label 'ltecomm'}
    triggers {
        cron ('H * * * 1-5')
    }
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'enter your maven goal')
    }
    options {
        timeout(time: 30, unit: 'Minutes')
    }
    stages{
        stage('SCM'){
            steps{
                git 'https://github.com/wakaleo/game-of-life.git'
            }
        }
        stage('build'){
            steps{
                sh script: "mvn ${params.MAVENGOAL}"
            }
        }
        stage('post-build'){
            steps{
                junit 'gameoflife-web/target/surefire-reports/*.xml'
                archieveArtifacts 'gameoflife-web/target/*.war'
            }
        }
    }
}