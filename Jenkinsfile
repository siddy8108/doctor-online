@Library("jhc-libs") _

pipeline {
    agent any

stages {
        stage('Maven Build') {
        steps {
            sh 'mvn clean package'
        }
    }

        stage('Tomcat Dev Deploy') {
            when {
                branch 'develop'
            }
        steps {
             echo "Deploying to Dev"
        }
    }
        stage('Tomcat Test Deploy') {
                        when {
                branch 'Test'
            }
        steps {
            echo "Deploying to Test"
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
}
post {
  success {
    cleanWs()
  }
}
}
