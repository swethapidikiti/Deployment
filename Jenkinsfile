pipeline{
    //Directives
    agent any
    tools {
        maven 'Maven'
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

        //Stage 3: Deploy
        stage('Delopy'){
            steps{
                echo 'deploying......'
            }
        }
    }
}