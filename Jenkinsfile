node {
  stage ('SCM checkout')
  {
    git 'https://github.com/rajputravisingh/maven-web-application.git'
  }
  stage ('Complile - Package')
  {
    sh 'mvn package'
  }

} 
