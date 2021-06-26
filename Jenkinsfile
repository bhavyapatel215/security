//declarative pipeline code

pipeline{
    agent any
    options { 
        quietPeriod(10) 
        buildDiscarder(logRotator(numToKeepStr: '3',daysToKeepStr: '3'))
    }
    triggers {
        pollSCM('* * * * *')
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
        stage('Deploy Container on dev_server') {
            environment { 
                dockerRUN = 'sh /home/ubuntu/dockerRUN.sh'
                }
            steps {
                sshagent(['dev_server']) {
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.14.10 ${dockerRUN}"

                }
            }
        }
    }
}
