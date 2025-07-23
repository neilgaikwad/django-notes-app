pipeline{
    agent {label 'Slave'}
    stages{
        stage('Code clone'){
            steps{
                git url: "https://github.com/neilgaikwad/django-notes-app.git", branch: "main"
                echo 'code cloned successfully'
            }
        }
        stage('Docker image build'){
            steps{
                sh "whoami"
                sh "docker build -t notes-app:2.0 ."
                echo 'image build successfully'
            }
        }
        stage('Docker image push'){
            steps{
                  withCredentials([usernamePassword(credentialsId: 'dockerCreds', passwordVariable: 'dockerhubpass', usernameVariable: 'dockerhubuser')]) {
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                sh "docker image tag notes-app:2.0 neilgaikwad/notes-app:2.0"
                sh "docker push neilgaikwad/notes-app:2.0"
                echo 'image pushed successfully to the Dockerhub'
                  }
            }
        }
    }
}
