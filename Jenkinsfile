//declarative pipeline code

pipeline{
    agent any
    options { 
        quietPeriod(30) 
    }

    tools {
        maven 'm3'
        jdk 'jdk8'
    }

    stages {
        stage('Clean Ws') {
            steps{
                cleanWs()
            }
        }
        stage('Git CheckoutOut'){
            steps{
                checkout scm
            }
        }
        stage ('Maven Package'){
            steps{
                sh 'mvn package'
            }   
        }

    }
}
