pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: '49a10f69-a8a3-4c31-8163-1713cefd4d4f', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.251:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
             }
            }
        }

        // Stage3 : Publish the artifacts to Nexus
        // stage ('Publish to Nexus'){
        //     steps {
        //         nexusArtifactUploader artifacts: 
        //         [[artifactId: "VinayDevOpsLab", 
        //         classifier: '', 
        //         file: "target/VinayDevOpsLab-0.0.4-SNAPSHOT.war", 
        //         type: 'war']], 
        //         credentialsId: '49a10f69-a8a3-4c31-8163-1713cefd4d4f', 
        //         groupId: "com.vinaysdevopslab", 
        //         nexusUrl: '172.20.10.251:8081', 
        //         nexusVersion: 'nexus3', 
        //         protocol: 'http', 
        //         repository: "VinaysDevOpsLab-SNAPSHOT", 
        //         version: "version: '0.0.4-SNAPSHOT"
             
        //     }
        // }
        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }



        stage ('Deploy'){
            steps {
                echo ' deploying......'
                }

            }
        
    }

}