pipeline{
    agent{
        label "slave"
    }
    stages{
        stage("cloning"){
            steps{
                echo"cloning repo to the server"
                git url:"https://github.com/Kunal-Pere/capstone-1.git", branch:"Production"
            }
        }
        stage("Building"){
            steps{
                echo"Building image through Dockerfile"
                sh "docker build -t kunal1010/cap1 ."
            }
        }
        stage("pushing on dockerhub"){
            steps{
                echo"pushing this image on dockerhub"
                withCredentials([usernamePassword(credentialsId:"DockerHub", usernameVariable:"dockeruser", passwordVariable:"dockerpass")]){
                sh "docker login -u ${env.dockeruser} -p ${env.dockerpass}"
                sh "docker push kunal1010/cap1"
                }
            }
        }
        stage("deploy in swarm stack"){
            steps{
                echo"deploying cap1 app"
                sh "docker stack deploy -c docker-compose.yml cap1_deployment"
            }
        }
    }
}
