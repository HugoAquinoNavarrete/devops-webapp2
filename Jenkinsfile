//START-OF-SCRIPT
//comment1
timeout(time: 60, unit: 'SECONDS') {
      node {
//    node('agent1') {
        def RELEASENAME = "webapp-1.0.war"

        properties([
            pipelineTriggers([pollSCM('H/5 * * * *')])
        ])
        
//        def GRADLE_HOME = tool name: 'gradle-4.10.2', type: 'hudson.plugins.gradle.GradleInstallation'
        def GRADLE_HOME = "/opt/gradle/gradle-4.10.2"
        sh "${GRADLE_HOME}/bin/gradle tasks"

        stage('Clone') {
            git url: 'https://github.com/HugoAquinoNavarrete/devops-webapp1.git'                
        }

        stage('Build') {
            sh "${GRADLE_HOME}/bin/gradle build -PwarName=${RELEASENAME} --info"
        }

        stage('Archive') {
            archiveArtifacts artifacts: "build/libs/${RELEASENAME}"
//              archiveArtifacts "${RELEASENAME}"
        }    
    }
}
//END-OF-SCRIPT
