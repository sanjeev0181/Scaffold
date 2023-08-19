pipeline {
     agent any
  
    stages {
        stage('Build') {    
            steps{
                echo "Building the code"
                //sh "git clone https://github.com/vemulavamsi/Scaffold.git"
                }
            }
        stage('Push Docker image to ECR') {
            steps {
                script{
                   // sh "docker rmi -f learning111"
                    sh "aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/g8i9m6o6"
                    sh "docker build -t learning111 ."

                    sh "docker tag learning111:latest public.ecr.aws/g8i9m6o6/learning111:latest"

                    sh "docker push public.ecr.aws/g8i9m6o6/learning111:latest"
                }
        }
    }
        stage('Pull Docker image from ECR') {
            steps {
                script{
                        // sh "docker pull ${buildProps.AWS_ACCOUNT_ID}.dkr.ecr.us-east-1.amazonaws.com/node-repo:${env.BUILD_NUMBER}"
                        //sh "docker rm -f learning111"
                        // sh "docker run -itd -p 3000:3000 --name learning111 ${buildProps.AWS_ACCOUNT_ID}.dkr.ecr.us-east-1.amazonaws.com/node-repo:${env.BUILD_NUMBER}"
                   // Removing existing image
                    sh "docker rmi -f learning111"
                    // Pulling latest version of docker image
                    sh "docker pull public.ecr.aws/g8i9m6o6/learning111:latest"
                    // creating container and port mapping
                    sh "docker run -itd -n vamsi-practice -p ${BUILD_NUMBER}:3000 public.ecr.aws/g8i9m6o6/learning111:latest"     
            }
        }
    }

 }
}