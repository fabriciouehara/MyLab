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
                nexusArtifactUploader artifacts: [[artifactId: 'FabricioDevOpsLab', classifier: '', file: 'target/FabricioDevOpsLab-0.0.9-SNAPSHOT.war', type: 'war']], credentialsId: 'Nexus', groupId: 'com.fabriciodevopslab', nexusUrl: '172.20.10.163:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'FabricioDevOpsLab-SNAPSHOT', version: '0.0.9-SNAPSHOT'
            }
        }

        // Stage 4: Print some informations
        stage ('Print environment variables') {
            steps (){
                echo "Artifact ID is '{$ArtifactId}'"
                echo "Version is '{$Version}'"
                echo "Group ID is '{}'"
                echo "Name is '{$Name}'"
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