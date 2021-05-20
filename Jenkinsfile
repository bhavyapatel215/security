node  {
    def Author = 'Atin Singh'

    stage('Clean WS') {
        sh 'echo "Cleaning WorkSpace"'
        cleanWs();

    }
    stage('Declartive Checkout'){
        checkout scm;
    }
    stage('Compile') {
        withMaven(jdk: 'jdk8', maven:'m3') {
            sh 'mvn compile'
        }
    }
     stage('Test') {
        withMaven(jdk: 'jdk8', maven:'m3') {
            sh 'mvn test'

        }
    }

     stage('Package') {
        withMaven(jdk: 'jdk8', maven:'m3') {
            sh 'mvn package'
        }
    }

}
