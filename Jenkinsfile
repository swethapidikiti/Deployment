pipeline{
    //Directives
    agent any
    tools {
        maven 'Maven'
    }
    // Declare environment variables and from that we can able to read values from pom.xml
    environment{
        ArtifactId = readMavenPOM().getArtifactId()
        Version = readMavenPOM().getVersion()
        Name = readMavenPOM().getName()
        GroupId= readMavenPOM().getGroupId()
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
                nexusArtifactUploader artifacts: 
                [[artifactId: 'SwethaLab',
                classifier: '',
                file: 'target/SwethaLab-0.0.4-SNAPSHOT.war',
                type: 'war']],
                credentialsId: 'e39b97a5-9d37-443b-9745-c3c2c6c75faa',
                groupId: 'com.Swethalab', nexusUrl: '172.20.10.99:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'SwethaLab_SNAPSHOT',
                version: '0.0.4-SNAPSHOT'
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