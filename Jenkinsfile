node {
  stage ('SCM checkout')
  {
    git 'https://github.com/rajputravisingh/maven-web-application.git'
  }
  
  stage('Sonar Analysis'){
    withSonarQubeEnv('SonarCloud'){
    //def mvnHome = tool 'maven3.3'
    //sh "'${mvnHome}'/bin/mvn sonar:sonar"
    sh 'mvn sonar:sonar'
    sh 'sleep 1m'

  }
}
  stage ('Complile - Package')
  {
    sh 'mvn clean package'
    archiveArtifacts 'target/maven-web-application.war'
  }
  
  stage ('Test')
  {
    sh 'mvn test'
  }
  
  stage ('Dev-Deploy')
  {
    sh 'sudo cp /target/maven-web-application.war /var/lib/tomcat8/webapps'
  }

  stage ('Email Notification') 
  {
    mail bcc: '', body: '''Hi Dev Team,

    The Build ${env.BUILD.NUMBER} has been successfully triggered, Code has been deployed to Dev Environment

    Regards,
    DevOps Team''', cc: '', from: '', replyTo: '', subject: 'echo Job Number ${env.JOB_NAME} success', to: 'ravisinghrajput005@gmail.com'
  }
  stage ('Slack-Notifiction')
  {
    slackSend baseUrl: 'https://hooks.slack.com/services/', 
    channel: '#project', color: 'good', 
    message: 'Welcome to Jenkins Slack channel', 
    tokenCredentialId: 'slack-notify'
  }

} 
