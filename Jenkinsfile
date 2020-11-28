pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        dir("C:\\\\Users\\\\56997\\\\Desktop\\\\diplomado-rafa\\\\ejemplo-maven") {
          sh 'mvn clean compile -e'
        }
      }
    }
    stage('test') {
      steps {
        dir("C:\\\\Users\\\\56997\\\\Desktop\\\\diplomado-rafa\\\\ejemplo-maven") {
          sh 'mvn clean test -e'
        }
      }
    }
    stage('jar') {
      steps {
        dir("C:\\\\Users\\\\56997\\\\Desktop\\\\diplomado-rafa\\\\ejemplo-maven") {
          sh 'mvn clean package -e'
        }
      }
    }
    stage('run') {
      steps {
        dir("C:\\\\Users\\\\56997\\\\Desktop\\\\diplomado-rafa\\\\ejemplo-maven") {
          withEnv(['JENKINS_NODE_COOKIE=dontkillme']) {
            sh """
 nohup java -jar build/DevOpsUsach2020-0.0.1.jar &
 """
          }
        }
      }
    }
    stage('curl') {
      steps {
        dir("C:\\\\Users\\\\56997\\\\Desktop\\\\diplomado-rafa\\\\ejemplo-maven") {
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
}