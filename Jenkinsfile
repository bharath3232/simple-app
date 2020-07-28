pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"

                    
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'simple-app', 
                            classifier: '', 
                            file: "target/simple-app-1.0.0.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'sonar', 
                    groupId: 'in.javahome', 
                    nexusUrl: '3.18.220.38:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: simple-app, 
                    version: '1.0.0'
                    }
            }
        }
    }
}
