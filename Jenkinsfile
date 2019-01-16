def CONTAINER_NAME="jenkins-pipeline"
def CONTAINER_TAG="latest"
def DOCKER_HUB_USER="scetin1337"
def HTTP_PORT="8090"

pipeline {
    agent none
    stages {

	stage('Non-Parallel Stage') {
	    agent {
                        label "master"
                }
        steps {
                echo 'This stage will be executed first'
                }
        }


        stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
                    agent {
                        label "Windows_Node"
                    }
                    steps {
                        echo "Task1 on Agent"
                    }

                }
                stage('Test On Master') {
                    agent {
                        label "master"
                    }
                    steps {
						echo "Task1 on Master"
					}
                }
            }
        }
	    
	stage('Push to Docker Registry'){
        withCredentials([usernamePassword(credentialsId: 'dockerHubAccount', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            pushToImage(CONTAINER_NAME, CONTAINER_TAG, USERNAME, PASSWORD)
        }
    }
    }
}
