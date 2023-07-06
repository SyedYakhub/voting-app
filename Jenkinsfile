pipeline{
    agent any
    stages{
        stage ('git repository checkout') {
            steps{
            
                //repository checkout
                sh 'git clone https://github.com/SyedYakhub/voting-app.git'

            }
        }
        stage ('build and push images to dockerhub'){
            steps{
                
                //dockerhub credetials
                withCredentials([string(credentialsId: 'DockerPasswd', variable: 'DockerPasswd')]) {
                
                sh "docker login -u yakhub4881 -p ${DockerPasswd}"

                
                //voter
                //build vote image
                sh "docker build -t $JOB_NAME-vote:v1.$BUILD_ID voting-app/vote"

                //tag image
                sh "docker tag $JOB_NAME-vote:v1.$BUILD_ID yakhub4881/$JOB_NAME-vote:v1.$BUILD_ID"
                
                //push image to dockerhub
                sh "docker push yakhub4881/$JOB_NAME-vote:v1.$BUILD_ID"

                
                //worker
                //build worker image
                sh "docker build --build-arg BUILDPLATFORM=linux/amd64 -t $JOB_NAME-worker:v1.$BUILD_ID voting-app/worker"

                //tag worker image
                sh "docker tag $JOB_NAME-worker:v1.$BUILD_ID yakhub4881/$JOB_NAME-worker:v1.$BUILD_ID"

                //push docker image
                sh "docker push yakhub4881/$JOB_NAME-worker:v1.$BUILD_ID "

                
                //result
                //build result image
                sh "docker build -t $JOB_NAME-result:v1.$BUILD_ID voting-app/result"

                //tag result image
                sh "docker tag $JOB_NAME-result:v1.$BUILD_ID yakhub4881/$JOB_NAME-result:v1.$BUILD_ID"

                //push result image
                sh "docker push yakhub4881/$JOB_NAME-result:v1.$BUILD_ID"
}
            }
        }
        
    }
}
