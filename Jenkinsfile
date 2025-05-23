pipeline {
        agent {
               label 'slave1'
               }
        stages {
                stage("SCM") {
                     steps {
                            git branch: 'main', url: 'https://github.com/lalit7773/dockerpush.git' 
                            }
                          }

                stage("build") {
                     steps {
                             sh 'sudo mvn clean package'
                             }
                           }
                stage("build-image"){
		   steps{
		        sh 'sudo docker build -t java-repo:$BUILD_TAG .'
			sh 'sudo docker tag java-repo:$BUILD_TAG lalit7773/pipeline-java:$BUILD_TAG'
			}
                 }
		stage("dockerlogin"){
		   steps{
		         withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_pass_var')]) {
			 sh 'sudo docker login -u lalit7773 -p ${docker_pass_var}'
			 sh 'sudo docker push lalit7773/pipeline-java:$BUILD_TAG'
			 }
		   }
                }
		stage("QAT TESTING") {
		     steps {
                              sh 'sudo docker rm -f $(sudo docker ps -a -q)'
		              sh 'sudo docker run -dt --name web8tom -p 8087:8080 lalit7773/pipeline-java:$BUILD_TAG'
                    }
               }
	       stage("test-website") {
	             steps {
		              sh 'sudo sleep 20'
		              sh 'sudo curl http://13.218.48.96:8087'
		       }
	       }
	       stage("approval-stage") {
	             steps {
		         script {
			          Boolean userInput = input(id: 'Proceed1', message: 'Do you want Promote build?',parameters: [[$class: 'BooleanParameterDefinition', defaultValue: true,description: '', name: 'Please confirm your agree with this']])
                                 echo 'userInput: ' + userInput
                                 }
                      }
               }
        }
}

