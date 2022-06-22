pipeline {
   agent any

   tools {
         maven 'Maven'
    }

   stages {
      stage("Git Checkout") {
          steps {
              script {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: "https://github.com/AyushiSinglaPrsnl/Assignment1.git"]]])
              }
          }
      }

      stage('Compile & Package') {      
        steps{
          script{
                sh """
                mvn clean compile -DskipTests=true
                mvn clean package -DskipTests=true
                """
        }  
      }                   
      }
      stage('Build') {      
        steps{
          script{
                sh """
                mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true -B -V
                """
        }  
      }                   
      }
      stage('Deploy') {      
        steps{
          script{
                sh """
                mvn -V -U -e clean deploy -Dsurefire.useFile=false
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
