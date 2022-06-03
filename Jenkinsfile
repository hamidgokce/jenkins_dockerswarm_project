pipeline {
    agent any
 
    stages {
        stage('Create ECR Repo') {
            steps {
                echo 'Creating ECR Repo for App'
            }
        }

        stage('Build App Docker Image') {
            steps {
        }

        stage('Push Image to ECR Repo') {
            steps {
                echo 'Pushing App Image to ECR Repo'
            }
        }

        stage('Create Infrastructure for the App') {
            steps {
                echo 'Creating Infrastructure for the App on AWS Cloud'
                }
            }
        }

        stage('Test the Infrastructure') {

             steps {
                 echo "Testing if the Docker Swarm is ready or not, by checking Viz App on Grand Master with Public Ip Address: ${MASTER_INSTANCE_PUBLIC_IP}:8080"
                     }
                   }
                
        stage('Deploy App on Docker Swarm'){
            steps {
            }
        }

        stage('Destroy the infrastructure'){
            steps{
            }
        }

    }

    post {
        always {
            echo 'Deleting all local images'
            sh 'docker image prune -af'
        }
        failure {

            echo 'Delete the Image Repository on ECR due to the Failure'
            sh """
                aws ecr delete-repository \
                  --repository-name ${APP_REPO_NAME} \
                  --region ${AWS_REGION}\
                  --force
                """
            echo 'Deleting Cloudformation Stack due to the Failure'
                sh 'aws cloudformation delete-stack --region${AWS_REGION} --stack-name ${AWS_STACK_NAME}'  
        }

    }

}
