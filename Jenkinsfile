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

//    stage('Publish') {
//      steps {
//        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
//      }
//  }

    stage('Packaging') {
      steps {
          script{
             docker.withRegistry("https://index.docker.io/v1/","dockerlogin"){
             def workerImage = docker.build("hugoaquinonavarrete/webapp:v${env.BUILD_ID}","./webapp")
             workerImage.push()
             workerImage.push("${env.BRANCH_NAME}")
          }
      }



//        sh '''pwd
//        cd ./docker
//        docker build -t hugoaquinonavarrete/webapp1-2021:$BUILD_ID
//        docker tag hugoaquinonavarrete/webapp1-2021:$BUILD_ID hugoaquinonavarrete/webapp1-2021:latest
//        docker images'''
    }
  }


  }
}
