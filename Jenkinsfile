pipeline {
  agent {
     docker {
          image 'node:18.16.0-alpine'
            }
        }
  stages {
    stage('Compile') {
      steps{
        sh 'mvn clean compile'
      }
    }

    stage('UnitTest') {
      steps{
        sh 'mvn clean test'
      }
    }
    
    stage('Package') {
      steps{
        sh 'mvn package'
     }
    }

    stage('Deliver') {
      steps{
        deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://18.233.163.71:9090/')], contextPath: null, war: 'target/calculator.war'
     }
    }

  }
}
