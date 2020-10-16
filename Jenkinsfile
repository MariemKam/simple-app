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
                            file: 'target/simple-app-3.0.0-SNAPSHOT.war', 
                            type: 'war']
                    ], 
                        credentialsId: 'c0e3bf3a-e883-4d09-9953-d8a2db8da1f0', 
                        groupId: 'in.javahome', 
                        nexusUrl: 'localhost:8082/#admin/', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'http://localhost:8082/repository/Sample_Test_Nexus_SNAP/', 
                        version: '3.0.0-SNAPSHOT'
                    }
            }
        }
    }
}
