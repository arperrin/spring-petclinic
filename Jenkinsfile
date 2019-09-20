pipeline {
    agent any
    tools {
        maven 'Maven 3.6.1'
    }
    stages { 
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/arperrin/spring-petclinic.git']]])                
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Jacoco') {
            steps {
                jacoco()
            }
        }
    }
    post {
        always {
            emailext (
                body: '${JELLY_SCRIPT,template="html"}',
                mimeType: 'text/html',
                subject: 'Jenkins $PROJECT_NAME # $BUILD_NUMBER - [$BUILD_STATUS]',
                to: 'aperrin726@gmail.com'
            )
        }
    }   
}