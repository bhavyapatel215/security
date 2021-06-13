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
        stage ('Build Docker Image '){
            steps{
                sh 'docker image build -t bhavyapatel215/myapp:1.0.0 .'
            }   
        }
        stage ('Docker Image Push'){
            steps{
                withCredentials([string(credentialsId: 'docker_hub_pass', variable: 'docker_hub_pass')]) {
                    sh "docker login -u bhavyapatel215 -p ${docker_hub_pass}"
                }
                sh 'docker push bhavyapatel215/myapp:1.0.0'
            }   
        }

    }
}
