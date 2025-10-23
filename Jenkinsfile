pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {
        stage('Build jar') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo "Building the Docker image ..."
                    withCredentials([usernamePassword(credentialsId: 'cred-docker-hub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t lllliamsi/demo-app:jma-2.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push lllliamsi/demo-app:jma-2.0'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the application ..."
                }
            }
        }
    }
}
