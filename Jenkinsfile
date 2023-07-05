pipeline{
    agent any
    stages{
        stage ('remove previously added repo'){
            steps{
                sh 'rm -rf voting-app*'
            }
        }
        stage ('git repository checkout') {
            steps{
                sh 'git clone https://github.com/SyedYakhub/voting-app.git'
            }
        }
        stage ('build and push images to dockerhub'){
            steps{
                //dockerhub credetials
                withCredentials([string(credentialsId: 'DockerPasswd', variable: 'DockerPasswd')]) {
                
                sh "docker login -u yakhub4881 -p ${DockerPasswd}"

                //remove exisiting docker images
                sh "docker rmi -f \$(docker images --format '{{.Repository}}:{{.Tag}}' | grep '$JOB_NAME-vote')"
                sh "docker rmi -f \$(docker images --format '{{.Repository}}:{{.Tag}}' | grep 'yakhub4881/$JOB_NAME-vote')"

                //build vote image
                sh "docker build -t $JOB_NAME-vote:v1.$BUILD_ID voting-app/vote"

                //tag image
                sh "docker tag $JOB_NAME-vote:v1.$BUILD_ID yakhub4881/$JOB_NAME-vote:v1.$BUILD_ID"
                
                //pudh image to dockerhub
                sh "docker push yakhub4881/$JOB_NAME-vote:v1.$BUILD_ID"
}
            }
        }
        
    }
}
