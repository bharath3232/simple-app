pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload War To Nexus'){
            steps{
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'simple-app', 
                            classifier: '', 
                            file: "target/simple-app-1.0.0.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'b4408069-1499-44ba-97ab-fd84e2998697',
                    groupId: 'in.javahome', 
                    nexusUrl: '3.18.220.38:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'simple-app', 
                    version: '1.0.0'
                    
            }
        }
    }
}
