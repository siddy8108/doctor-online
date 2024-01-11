@Library("jhc-libs") _

pipeline {
    agent any

    stages {
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Upload Artifacts") {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'doctor-online', classifier: '', file: 'target/doctor-online.war', type: 'war']],
                    credentialsId: 'nexus3',
                    groupId: 'in.javahome',
                    nexusUrl: 'http://172.31.36.137:8081', // Fix the protocol
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'do-release',
                    version: '1.3'
            }
        }
        stage('Tomcat Dev Deploy') {
            steps {
                tomcatDeploy ("172.31.37.255", "ec2-user", "tomcat-dev", "doctor-online.war")
            }
        }
    }

    post {
        success {
            cleanWs()
        }
    }
}
