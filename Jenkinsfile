pipeline{
    agent { label 'ltecomm'}
    triggers {
        cron ('H * * * 1-5')
    }
    stages{
        stage('SCM'){
            steps{
                git 'https://github.com/wakaleo/game-of-life.git'
            }
        }
        stage('build'){
            steps{
                sh script: 'mvn clean package'
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