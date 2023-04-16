pipeline{
    //Directives
    agent any

    tools {
        maven 'maven'
    }

    environment {
        artifactId = readMavenPom().getArtifactId()
        version = readMavenPom().getVersion()
        name = readMavenPom().getName()
        groupId = readMavenPom().getGroupId()
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

        // Stage 4 : Print some information
        stage('Print environment variables') {
            steps {
                echo "artifactId is '{$artifactId}'"
                echo "version is '{$version}'"
                echo "groupId is '{$groupId}'"
                echo "name is '{$name}'"
            }
        }

        // Stage 5 : Publish the artifacts to Nexus
        stage ('Publish to Nexus') {
            steps {
                script {
                    def nexusRepo = version.endsWith("SNAPSHOT") ? "MyLab-SNAPSHOT" : "MyLab-RELEASE"

                    nexusArtifactUploader artifacts: 
                    [[artifactId: "${artifactId}", 
                    classifier: '',
                    file: "target/${artifactId}-${version}.war",
                    type: 'war']],
                    credentialsId: '3e2d15ff-b405-454e-97cf-f7b6a284fce5',
                    groupId: "${groupId}",
                    nexusUrl: '172.20.10.219:8081',
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${nexusRepo}", 
                    version: "${version}"
                }
            }
        }

         // Stage 6 : Deploying
        stage ('Deploy'){
            steps {
                echo ' deploying......'

            }
        }

        
        
    }

}
