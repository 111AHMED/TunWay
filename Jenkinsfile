pipeline {
    environment {
    registry = 'tunops/tunway'
    registryCredential = 'docker'
    dockerImage = ''
  }
    agent any 
    stages {
    stage('Mail Notification') {
     steps {
        echo 'Sending Mail'
        mail bcc: '',
        body: 'Jenkins Build Started',
        cc: '',
        from: '',
        replyTo: '',
        subject: 'Jenkins Job',
        to: 'tunisiantuniops@gmail.com'
      }
    }
    stage('Git') {
      steps {
        echo 'Cloning'
        git branch: 'master', url: 'https://github.com/TunOps/TunWay.git/'
      }
    }
    stage('Building our image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy image to Docker Hub') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }

      }
        
    }
      stage('Cleaning up Docker Image') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    
      }
}
}
