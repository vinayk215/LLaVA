pipeline{
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/vinayk215/LLaVA'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('SonarQube analysis') {
        steps{
        withSonarQubeEnv('sonarqube-9.9.2') { 
        sh "mvn sonar:sonar"
    }
        }
        }
stage("Quality Gate") {
            steps {         
                    waitForQualityGate abortPipeline: true
            }     
            }
    }
}
