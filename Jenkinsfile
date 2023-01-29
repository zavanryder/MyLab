pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the source code to Sonarqube
        // stage ('Sonarqube Analysis'){
        //     steps {
        //         echo ' Source code published to Sonarqube for SCA......'
        //         withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
        //              sh 'mvn sonar:sonar'
        //         }

        //     }
        // }
        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                script {

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "VinaysDevOpsLab-SNAPSHOT" : "VinaysDevOpsLab-RELEASE"

                nexusArtifactUploader artifacts: 
                [[artifactId: "VinayDevOpsLab", 
                classifier: '', 
                file: "target/VinayDevOpsLab-0.0.1-SNAPSHOT.war", 
                type: 'war']], 
                credentialsId: '49a10f69-a8a3-4c31-8163-1713cefd4d4f', 
                groupId: "com.vinaysdevopslab", 
                nexusUrl: '172.20.10.251:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "VinaysDevOpsLab-SNAPSHOT", 
                version: "version: '0.0.1-SNAPSHOT"
             }
            }
        }


        stage ('Deploy'){
            steps {
                echo ' deploying...'
                }

            }
        
    }

}