pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/HugoAquinoNavarrete/devops-webapp2', branch: 'master')
      }
    }

    stage('Build') {
      steps {
        sh '''whoami
date
echo $PATH
pwd
ls -la
ls -l /var/jenkins_home/*.gz
./gradlew build --info'''
      }
    }


    stage('Build') {
      sh "${GRADLE_HOME}/bin/gradle build -PwarName=${RELEASENAME} --info"
    }

    stage('Archive') {
      archiveArtifacts artifacts: "build/libs/${RELEASENAME}"
    }


//    stage('Publish') {
//      steps {
//        archiveArtifacts(artifacts: 'builds/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
//      }
//   }

  }
}
