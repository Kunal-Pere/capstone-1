pipeline{
    agent{
        label "slave"
    }
    stages{
        stage("cloning"){
            steps{
                echo"cloning repo to the server"
                git url:"", branch:"main"
            }
        }
        stage("Building"){
            steps{
                echo"Building image through Dockerfile"
                sh "docker build -t kunal1010/myschool ."
            }
        }
        stage("pushing on dockerhub"){
            steps{
                echo"pushing this image on dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerhub", usernameVariable:"dockeruser", passwordVariable:"dockerpass")]){
                sh "docker login -u ${env.dockeruser} -p ${env.dockerpass}"
                sh "docker push kunal1010/myschool"
                }
            }
        }
        stage("deploy"){
            steps{
                echo"deploying myschool app"
                sh "docker run -itd -p 82:80  kunal1010/myschool"
            }
        }
    }
}
