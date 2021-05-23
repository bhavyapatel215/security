//declarative pipeline code

pipeline{
    agent any
    
    environment {
        APP_HOME='/var/www/html'
        PRAGRA_BATCH='devops'
    }

    options {
        quitePeriod(10)
        
    }
    parameters {
        choice(name: 'ENVIRONMENT TO DEPLOY', choice: ['Windows', 'Linux', 'MacOS'], description: 'Select a Env to deploy')
    }
    triggers {
        pollSCM('* * * * *')
    }

     tools{
        maven  'm3'
        jdk 'jdk8'
    }

    stages{
        stage('Code checkout'){
            environment{
                GIT_REPO='https://github.com/bhavyapatel215/security.git'
        }
         steps {
                git "${GIT_REPO}"
            }
    }
     stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    post {
        changed {
            echo '**** Something is WRONG !! ****** '
            echo "${BRANCH_NAME}  : ${JOB_NAME}"
        }
     }

}
}
