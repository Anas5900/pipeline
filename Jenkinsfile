pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }
         stage('Build') {
            steps {
                sh '/usr/local/bin/docker build -t anas59/exo7:latest .'
            }
        }
stage('Login to Docker Hub') { 

            steps { 

                withCredentials([usernamePassword( 

                credentialsId: 'id_dockerhub', 

                usernameVariable: 'USERNAME', 

                passwordVariable: 'PASSWORD' 

                )]) { 

                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin' 

                } 

            } 

        }
stage('Push') {
            steps {
                sh 'docker push anas59/exo7:latest'
            }
        } 
stage('Start') {
            steps {  
                sh 'docker compose up'
            }
        }

}
post { 

        always { 

            echo 'Cleaning workspace...' 

            cleanWs() 

        } 

    }
}
