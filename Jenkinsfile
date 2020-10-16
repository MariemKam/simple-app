pipeline {
    agent any
    tools {
        maven 'maven3.6.3'
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
                
                def mavenPom = readMavenPom file: 'pom.xml'
                def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"
                
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
