pipeline {
  agent any
  tools{
    mvn 'Maven 3.6.1'
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean deploy'
      }
    }
  }
}