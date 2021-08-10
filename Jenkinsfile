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

        stage ('Publish to Nexus Repo'){
            scripts{

            nexusArtifactUploader artifacts:
            [[artifactId: 'DemoDevOpsLab', classifier: '', file: 'target/DemoDevOpsLab-0.0.2-SNAPSHOT.war',
            type: 'war']], 
            credentialsId: '19261fcf-f931-44e1-9a37-5ad9fa1b60f9',
            groupId: 'com.vinaysdevopslab', 
            nexusUrl: '172.20.10.213:8081', 
            nexusVersion: 'nexus3', 
            protocol: 'http', 
            repository: 'DemoDevopsLabs-SNAPSHOT', 
            version: '0.0.2-SNAPSHOT'    
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

        
        
    }

}