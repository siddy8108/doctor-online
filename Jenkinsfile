@Library("jhc-libs") _

pipeline {
    agent any

stages {
        stage('Maven Build') {
        steps {
            sh 'mvn clean package'
        }
    }
        stage ("Upload Artifacts"){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'doctor-online', classifier: '', file: 'target/doctor-online.war', type: 'war']], 
                    credentialsId: 'nexus3', 
                    groupId: 'in.javahome', 
                    nexusUrl: '172.31.36.137:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'do-release', 
                    version: '1.3'
            }
        }
        stage('Tomcat Dev Deploy') {
            when {
                branch 'develop'
            }
        }
    }
        stage('Tomcat Prod Deploy') {
                        when {
                branch 'main'
            }
        steps {
             echo "Deploying to Prod"
        }
    }
    }
post {
  success {
    cleanWs()
  }
}
