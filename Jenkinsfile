pipeline {  
    environment {
      registry = "valdirmorales/mobead_image_build"
      registryCredential = 'dockerhub'
      dockerImage = ''
      export DOCKER_USERNAME="valdirmorales"
      export DOCKER_PASSWORD="Teste1971"
      echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
    }
    agent any 
    stages { 
        stage('Lint Dockerfile'){ 
            steps{
                echo "Pipeline Usando Jenkinsfile"
                sh 'docker run --rm -i hadolint/hadolint < Dockerfile'
            }
        }
        stage('Build image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Delivery image') {
            steps{
                script {
                  docker.withRegistry('https://registry-1.docker.io/v2/', 'dockerhub') {
                   dockerImage.push("$BUILD_NUMBER")
                  }
                }
            }
        }
    } 
}
