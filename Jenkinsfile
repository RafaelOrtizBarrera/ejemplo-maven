pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        
          sh 'mvn clean compile -e'
        
      }
    }
    stage('test') {
      steps {
        
          sh 'mvn clean test -e'
        
      }
    }
    stage('jar') {
      steps {
          sh 'mvn clean package -e'
      }
    }
    stage('SonarQube') {
      steps {
        withSonarQubeEnv(installationName: 'sonar-local') { // You can override the credential to be used
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
        }
      }
    }
    stage('run') {
      steps {
        
          withEnv(['JENKINS_NODE_COOKIE=dontkillme']) {
            sh """
 nohup java -jar build/DevOpsUsach2020-0.0.1.jar &
 """
          }
        
      }
    }
    stage('curl') {
      steps {
        
          echo 'Esperando a que inicie el servidor'
          sleep(time: 10, unit: "SECONDS")
          script {
            final String url = "http://localhost:8081/rest/mscovid/test?msg=testing"
            final String response = sh(script: "curl -X GET $url", returnStdout: true).trim()

            echo response
          }
        
      }
    }
  }
}