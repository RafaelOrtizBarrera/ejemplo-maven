pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        //dir("/Users/rafael/cursos-dev/diplomado-devops/ci-cd/ejemplo-maven") {
          sh 'mvn clean compile -e'
        //}
      }
    }
    stage('test') {
      steps {
        //dir("/Users/rafael/cursos-dev/diplomado-devops/ci-cd/ejemplo-maven") {
          sh 'mvn clean test -e'
        //}
      }
    }
    stage('jar') {
      steps {
        //dir("/Users/rafael/cursos-dev/diplomado-devops/ci-cd/ejemplo-maven") {
          sh 'mvn clean package -e'
        //}
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
        //dir("/Users/rafael/cursos-dev/diplomado-devops/ci-cd/ejemplo-maven") {
          withEnv(['JENKINS_NODE_COOKIE=dontkillme']) {
            sh """
 nohup java -jar build/DevOpsUsach2020-0.0.1.jar &
 """
          }
        //}
      }
    }
    stage('curl') {
      steps {
        //dir("/Users/rafael/cursos-dev/diplomado-devops/ci-cd/ejemplo-maven") {
          echo 'Esperando a que inicie el servidor'
          sleep(time: 10, unit: "SECONDS")
          script {
            final String url = "http://localhost:8081/rest/mscovid/test?msg=testing"
            final String response = sh(script: "curl -X GET $url", returnStdout: true).trim()

            echo response
          }
        //}
      }
    }
  }
}