pipeline {
   agent {label 'centos7-02'}
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
            sh "docker run -d -p 8090:8080 --name tomcatapp tomcatwebapp:${env.BUILD_ID}"
         }
      }
   }
   post {
      always {
         mail to: 'kohn.om@gmail.com',
            subject: "Build Status: ${currentBuild.fullDisplayName} - ${currentBuild.result}",
            body: "${env.BUILD_URL} has result ${currentBuild.result}"
      }  
   }
}
 
