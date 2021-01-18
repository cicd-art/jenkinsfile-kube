pipeline {
    agent any

    environment{
        DOCKER_TAG = getDockerTag()
    }

    stages {
        stage ('build docker image')
        {
            steps{
                sh 'docker build -t sachin13579/nodeapp:${DOCKER_TAG} .'
            }
        }

	  stage ("docker build push")
        {
            
            withCredentials([string(credentialsId: 'docker-cred', variable: 'dockerhubpwd')]) {
                sh "docker login -u sachin13579 -p ${dockerhubpwd}"
                sh "docker push sachin13579/nodeapp:${DOCKER_TAG}"
            }
        }



    }
}


def getDockerTag() {
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
