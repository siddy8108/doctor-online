@Library("jhc-libs") _

pipeline {
    agent any

stages {
    stage('Code Checkout') {
        steps {
            git branch: 'main', credentialsId: 'github', url: 'https://github.com/siddy8108/doctor-online/'
        }
    }
    stage('Maven Build') {
        steps {
            sh 'mvn clean package'
        }
    }
        stage('Tomcat Dev Deploy') {
        steps {
            tomcatDeploy("172.31.37.255","ec2-user","tomcat-dev","doctor-online.war")
        }
    }
        }
post {
  success {
    cleanWs()
  }
}
}
