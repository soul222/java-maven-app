pipeline {
    agent any
    
    tools {
        maven 'maven-3.9'
    }
    
    stages {
        stage('Build Jar') {
            steps {
                sh 'mvn package'
            }
        }
        
        stage('Build Image') {
            steps {
                script {
                    echo "Building the Docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t azeshion21/demo-app:jma-2.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin"'
                        sh 'docker push azeshion21/demo-app:jma-2.0'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
