// need to install this in jenkins server before running the pipe - sudo yum install libatomic -y

pipeline {
    agent any

    tools {
        nodejs 'node18'
    }
    
    environment {
        IMAGE_NAME = "sujanvijay/nodejs-app"
        CONTAINER_NAME = "nodeapp-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/sujanvijay/nodejs_artifact_for_jenkins_webserver.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Create Artifact') {
            steps {
                sh 'npm pack'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }


        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true
                docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME:latest
                sleep 60
                docker stop nodecontainer
                docker rm nodecontainer
                '''
            }
        }

    }
}
