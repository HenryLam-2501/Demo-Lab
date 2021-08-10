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

        // stage ('Publish to Nexus Repo'){
        //     steps{
        //     nexusArtifactUploader artifacts:
        //     [[artifactId: 'DemoDevOpsLab', 
        //     classifier: '', 
        //     file: 'target/DemoDevOpsLab-0.0.3-SNAPSHOT.war',
        //     type: 'war']], 
        //     credentialsId: '19261fcf-f931-44e1-9a37-5ad9fa1b60f9',
        //     groupId: 'com.vinaysdevopslab', 
        //     nexusUrl: '172.20.10.213:8081', 
        //     nexusVersion: 'nexus3', 
        //     protocol: 'http', 
        //     repository: 'DemoDevopsLabs-SNAPSHOT', 
        //     version: '0.0.3-SNAPSHOT'    
        // }

        // }
        stage ('Publish to Nexus'){
            steps {
                script {

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "DemoDevopsLabs-SNAPSHOT" : "DemoDevOpsLabs-RELEASE"

                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: '19261fcf-f931-44e1-9a37-5ad9fa1b60f9',
                // credentialsId: '35e9b26e-269a-4804-a70d-6b2ec7a608ce', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.213:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
             }
            }
        }
    
        // Stage3 : Publish the source code to Sonarqube
        stage ('Sonarqube Analysis'){
            steps {

                echo 'deploying......'
                // echo ' Source code published to Sonarqube for SCA......'
                // withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                //      sh 'mvn sonar:sonar'
                // }

            }
        }

        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }

        
        
    }

}