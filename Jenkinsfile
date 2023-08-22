pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("build jar") {
            steps {
                script {
                    echo "building the application..."
                    sh 'mvn package'
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'hub.docker.com', passwordVariable: 'PASS', usernameVariable: 'USER')])
                    sh 'mv java-maven-app-1.1.0-SNAPSHOT.jar full-pipeline'
                    sh 'docker build -t tiusoro/full-pipeline:jma-1.0 .' 
                    sh "echo $PASS | docker login -u $USER --password-stdin" 
                    sh 'docker push tiusoro/full-pipeline:jma-1.0' 
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying the application..."
                    
                }
            }
        }

    }
}
