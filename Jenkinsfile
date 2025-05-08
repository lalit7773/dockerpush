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

    }
 }

