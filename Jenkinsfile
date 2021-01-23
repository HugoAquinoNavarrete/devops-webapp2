pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/HugoAquinoNavarrete/devops-webapp2', branch: 'main')
      }
    }

    stage('Build') {
      steps {
        sh '''RELEASE=webapp.war
pwd
/bin/bash/ gradlew build -PwarName=$RELEASE --info
ls -la build/libs
cp ./build/libs/$RELEASE ./docker'''
      }
    }

//    stage('Publish') {
//      steps {
//        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
//      }
//  }

//    stage('Packaging') {
//      steps {
//        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
//      }
//  }


  }
}
