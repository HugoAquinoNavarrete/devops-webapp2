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
        sh '''RELEASE=webapp-1.0.war
pwd
/bin/bash gradlew build -PwarName=$RELEASE --info
ls -la build/libs
cp build/libs/$RELEASE ./docker'''
      }
    }

    stage('Packaging') {
      steps {
        sh '''pwd
        cd ./docker
        docker build -t hugoaquinonavarrete/webapp1-2021:$BUILD_ID .
        docker tag hugoaquinonavarrete/webapp1-2021:$BUILD_ID hugoaquinonavarrete/webapp1-2021:latest
        docker images'''
      }
    }

//    stage('Publish') {
//      steps {
//        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
//      }
//  }

    stage('Publish') {
//      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerlogin', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
        sh '''pwd
        cd ./docker
        docker login -u="$DOCKER_USERNAME" -p="$DOCKER_PASSWORD"
        docker push hugoaquinonavarrete/webapp1-2021:$BUILD_ID
        docker push hugoaquinonavarrete/webapp1-2021:latest
        '''
      }
    }


  }
}
