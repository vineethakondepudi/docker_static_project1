pipeline{
agent any
      environment {
        DOCKERHUB_USER = "vineethakondepudi"
        DOCKERHUB_REPO = "docker_static_project"
    }

stages{
stage("Build Docker Image"){
steps{
sh "docker build -t ${DOCKERHUB_USER}/${DOCKERHUB_REPO}:latest ."
}
}
          stage("Push to Docker Hub") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_static_project', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh "docker push ${DOCKERHUB_USER}/${DOCKERHUB_REPO}:latest"
                }
            }
        }

stage("Run Container"){
steps{
   sh "docker rm -f docker_static_project1 || true"
sh "docker run -d --name docker_static_project1 -p 8084:80 ${DOCKERHUB_USER}/${DOCKERHUB_REPO}:latest"
}
}
}
}
