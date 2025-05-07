pipeline {
        agent {
               label 'slave1'
               }
        stages {
                stage("SCM") {
                     steps {
                            git 'https://github.com/lalit7773/dockerpush.git' 
                            }
                          }

                stage("build") {
                     steps {
                             sh 'sudo mvn clean package'
                             }
                           }
                stage("build-image") {
                     steps {
                             sh ''
                             sh ''
                             }
                }
                stage("dockerlogin") {
                     steps { 
		             withCredentials([string(credentialsId: 'dockerhub_pass', variable: 'dockerhub_pass_var')]) {
			     sh 'docker login -u lalit7773 -p ${dockerhub_pass_var}'
			     sh 'docker push lalit7773/pipeline-java:$BUILD_TAG'
			     }
		     }
		      
		}
		stage("QAT TESTING") {
		     steps {  
		              sh 'sudo docker run -dit -p 8080:8080 --name web1tom lalit7773/pipeline-java:$BUILD_TAG'
 		              sh ''
                    }
	    }
        }
}

