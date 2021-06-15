pipeline{
    //Directives
    agent any
    tools {
        maven 'Maven'
    }
    // Declare environment variables and from that we can able to read values from pom.xml
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId= readMavenPom().getGroupId()
    } 

    stages {
        //Specify various stage with in  stages
        stage('Build') {
            steps{
                sh 'mvn clean install package'
            }
        }
        // Stage 2: Testing
        stage('Test'){
            steps{
                echo 'testing.......'
            }
        }
        //Stage 3: Publishing build artifacts to Nexus repository
         stage('Publish the artifacts to Nexus'){
            steps{
                script{
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "SwethaLab_SNAPSHOT" : "SwethaLab-Release"
                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}",
                classifier: '',
                file: "target/${ArtifactId}-${Version}.war",
                type: 'war']],
                credentialsId: 'e39b97a5-9d37-443b-9745-c3c2c6c75faa',
                groupId: "${GroupId}",
                nexusUrl: '172.20.10.99:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: "${NexusRepo}",
                version: "${Version}"
            }
            }
        }

        //Stage 4: Print some information
        stage('Print Environment variables'){
            steps{
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }
        //Stage 5: Deploy
        stage('Delopy'){
            steps{
                echo 'deploying......'
            }
        }
    }
}