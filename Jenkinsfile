pipeline {
  agent {
     docker {
        image 'maven:3.9.0-eclipse-temurin-11'
        args '-v $HOME/.m2'
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
