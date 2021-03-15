node {
  stage ('SCM checkout')
  {
    git 'https://github.com/rajputravisingh/maven-web-application.git'
  }
  stage ('Complile - Package')
  {
    sh 'mvn package'
  }
  stage('SonarQube Analysis') {
      withSonarQubeEnv('Sonar') { 
      sh "${mvnHome}/bin/mvn sonar:sonar"
      }
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
