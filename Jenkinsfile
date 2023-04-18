pipeline{
agent any
  stages{
    stage("git checkot"){
      steps{
      git branch: 'main', credentialsId: '5', url: 'https://github.com/montfortthomas/new-colloge-project-.git'
      }
    }
    stage("maven build") {
      steps {
         sh "mvn clean package"
         sh "mv target/*.war target/myweb.war"
      }
    
    } 
    
    stage("tomcat dep") {
      
      steps {
      sshagent(['tomcat-file']) {
          sh """
             scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@43.204.32.91:/opt/tomcat8/wwbapps/
             
             ssh ec2-user@43.204.32.91 /opt/tomcat8/bin/shutdown.sh
        
             ssh ec2-user@43.204.32.91 /opt/tomcat8/bin/startup.sh          
              """ 
      }
      }
    
    }
    
  }
}
