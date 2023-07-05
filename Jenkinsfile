pipeline{
    agent any
    stages{
        stage ('git repository checkout') {
            steps{
                sh 'git clone https://github.com/SyedYakhub/voting-app.git'
            }
        }
        stage ('build and push images to dockerhub'){
            steps{
                //dockerhub credetials
                withCredentials([usernameColonPassword(credentialsId: 'DockerPasswd', variable: 'DockerPasswd')]) {
                
                sh """
                        echo \${DockerPasswd} | docker login -u yakhub4881 --password-stdin
                        // Additional Docker commands for building and pushing images
                    """

                //build vote image
                sh "docker build -t $JOB_NAME-vote:V1.$BUILD_ID -f voting-app/vote/Dcokerfile"

                //tag image
                sh "docker tag $JOB_NAME-vote:V1.$BUILD_ID yakhub4881:$JOB_NAME-vote:V1.$BUILD_ID"
                
                //pudh image to dockerhub
                sh "docker push yakhub4881:$JOB_NAME-vote:V1.$BUILD_I"
}
            }
        }
        
    }
}
