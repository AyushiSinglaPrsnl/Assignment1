pipeline {
   agent any

   tools {
         maven 'maven'
         jdk 'java'
    }

   stages {
      stage("Git Checkout") {
          steps {
              script {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: "https://github.com/AyushiSinglaPrsnl/Assignment1.git"]]])
              }
          }
      }

    stage ('Build') {      
      steps{
        script{
                sh """
                mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true -B -V
                """
        }  
      }                   
   }
   }
   post {
       always {
           cleanWs()
       }
   }
}
