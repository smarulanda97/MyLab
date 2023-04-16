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
        stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                // withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                    //  sh 'mvn sonar:sonar'
                // }

            }
        }

        // Stage 4 : Publish the artifacts to Nexus
        stage ('Publish to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '3e2d15ff-b405-454e-97cf-f7b6a284fce5', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.219:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'MyLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
            }
        }

         // Stage 5 : Deploying
        stage ('Deploy'){
            steps {
                echo ' deploying......'

            }
        }

        
        
    }

}
