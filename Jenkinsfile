pipeline {
    agent any

    tools {
        maven 'maven-3.9'
    }

    stages {
        stage('Build jar') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo "Building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t azevyn/demo-app:1ma.2.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push azevyn/demo-app:1ma.2.0'
                    }
                }
            }
        }

        // stage('Deploy') { ... }
    }
}
