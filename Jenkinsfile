pipeline {
   agent {label 'ctp-docker-node1'}
   stages{
      stage('Build'){
         steps{
            sh "/opt/apache-maven-3.5.4/bin/mvn clean package"
            sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
         }
      }
      stage('Deployment'){
         steps{
            sh "docker rm -vf tomcatapp || true"
            sh "docker run -d -p 8085:8080 --name tomcatapp tomcatwebapp:${env.BUILD_ID}"
         }
      }
   }
}
 
