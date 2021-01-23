pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/HugoAquinoNavarrete/devops-webapp2', branch: 'main')
      }
    }

    stage('Display') {
      steps {
        sh '''whoami
date
echo $PATH
pwd
ls -la
ls -l /var/jenkins_home/*.gz
/bin/bash gradlew build --info'''
      }
    }

    stage('Publish') {
      steps {
        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
      }
   }

  }
}
