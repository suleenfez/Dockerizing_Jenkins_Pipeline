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
		
	stage('Initialize'){
		def dockerhome=tool 'docker'
		env.PATH="${dockerHome}/bin:${env.PATH}"
	}
	
        stage ('Push to Docker Registry'){
	      withCredentials([usernamePassword(credentialsId:'dockerHubAccount',usernameVariable: 'USERNAME',
						passwordVariable: 'PASSWORD')]) {
		      pushToImage(CONTAINER_NAME,CONTAINER_TAG,USERNAME,PASSWORD)
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
		
		
	}	
		
    
    }
}
