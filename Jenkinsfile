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
     stage('Email'){
        emailext body: 'Build run complete!', subject: 'Jenkins Build Complete!', to: 'kohn.om@gmail.com'
     }
   }
}
 
