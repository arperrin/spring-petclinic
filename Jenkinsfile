pipeline {
  agent any
  tools{
    maven 'Maven 3.6.1'
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean deploy -Dmaven.skip.tests=true'
      }
    }
  }
}