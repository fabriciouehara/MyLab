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
                sh 'which mvn'
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
        
        // Stage 3: Publish the artefacts to Nexus
        stage ('Publish to Nexus'){
            steps(){
                nexusArtifactUploader artifacts: [[artifactId: 'FabricioDevOpsLab', classifier: '', file: 'target/FabricioDevOpsLab-0.0.10-SNAPHOT.war', type: 'war']], credentialsId: 'Nexus', groupId: 'com.fabriciodevopslab', nexusUrl: '172.20.10.163:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'FabricioDevOpsLab-SNAPSHOT', version: '0.0.10-SNAPHOT'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
        stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                //withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                //     sh 'mvn sonar:sonar'
                //}

            }
        }

        
        
    }

}