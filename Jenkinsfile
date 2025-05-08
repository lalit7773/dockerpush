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
      
    }
 }

