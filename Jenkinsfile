pipeline
{
    agent any
    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Aniket0258/node-todo-cicd.git", branch: "master"
                 echo "code copied"
            }
           
            
        }
        stage("build & test") {
            steps {
                sh "docker build . -t node-app"
                
                echo"code build & test"
            }
            
        }
        stage("push to repo") {
            steps {
                  echo "code push to repo"
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerHubpass", usernameVariable: "dockerHubuser")]) {
              sh "docker login -u ${env.dockerHubuser} -p ${env.dockerHubpass}"
        // Other Docker-related commands can follow here, securely using the logged-in credentials
              sh "docker tag node-app ${env.dockerHubuser}/node-app:latest "
              sh "docker push ${env.dockerHubuser}/node-app:latest  "
    }
}

        
        }
        stage("deployed") {
            steps {
                sh "docker-compose down && docker-compose up  -d"
                echo "code deployed"
                
            }
            
        }
        
        
    }
}
