pipeline {
    agent any
    tools {        
        maven 'Maven 3.6.1'
    }
    stages { 
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Publish To Nexus') {            
            steps {
                script {
                    def pom = readMavenPom file: 'pom.xml'
                    def version = pom.version + "-${BUILD_NUMBER}"
                    def artifact = "${WORKSPACE}/target/" + pom.build.finalName + ".jar"
                    
                    nexusPublisher nexusInstanceId: 'Nexus', 
                        nexusRepositoryId: 'perrin', 
                        packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: "jar", filePath: "${artifact}"]], 
                        mavenCoordinate: [artifactId: pom.artifactId, groupId: pom.groupId, packaging: pom.packaging, version: "${version}"]]]
                }
            }
        }
    }
}