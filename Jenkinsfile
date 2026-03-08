pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/sujanvijay/nodejs_artifact_for_jenkins_webserver.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodeapp .'
            }
        }

        stage('Run Container for 1 Minute') {
            steps {
                sh '''
                docker run -d --name nodecontainer nodeapp
                // sleep 60
                // docker stop nodecontainer
                // docker rm nodecontainer
                // '''
            }
        }
    }
}
