pipeline{
    agent any;
    stages{
        stage("code"){
            steps{
                git url :"https://github.com/subhomit-sudo/two-tier-flask-app.git" , branch: "master"
            }
        }
        stage("depoly"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("push to DockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"DockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                    )]){
                        
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                    sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
                
            }
        }
        stage("test"){
            steps{
                echo ("tester test case likh ke dega")
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
