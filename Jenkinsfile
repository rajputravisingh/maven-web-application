node {
  stage ('SCM checkout')
  {
    git 'https://github.com/rajputravisingh/maven-web-application.git'
  }
  stage ('Complile - Package')
  {
    sh 'mvn package'
  }
  stage ('Email Notification') 
  {
    mail bcc: '', body: '''Hi Dev Team,

    "The Build ${env.BUILD.NUMBER} has been successfully triggered, Code has been deployed to Dev Environment"

     Regards,
     DevOps Team''', cc: '', from: '', replyTo: '', subject: 'Build', to: 'ravisinghrajput005@gmail.com'
  }

} 
