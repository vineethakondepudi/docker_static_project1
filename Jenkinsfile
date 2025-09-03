pipeline{
agent any
stages{
stage("Build Docker Image"){
steps{
sh "docker build -t docker_static_project1 ."
}
}
stage("Run Container"){
steps{
sh "docker run -d -p 8083:80 docker_static_project1"
}
}
}
}
