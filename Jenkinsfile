pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-staging-demo"
        CONTAINER_NAME = "staging-container"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

       stage('Stop Existing Container') {
    steps {
        bat "docker stop %CONTAINER_NAME% || exit 0"
        bat "docker rm %CONTAINER_NAME% || exit 0"
    }
}

stage('Deploy to Staging') {
    steps {
        bat """
        docker run -d ^
        --name %CONTAINER_NAME% ^
        -p 5000:5000 ^
        %IMAGE_NAME%:latest
        """
    }
}

stage('Post-Deployment Verification') {
    steps {
        bat "curl http://localhost:5000"
     }
    }
   
  }
}
