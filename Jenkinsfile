pipeline {
  agent any
 
  tools {
  maven 'MAVEN_HOME'
  }
  stages {
    stage ('Build') {
      steps {
      sh 'clean install -f MyWebApp/pom.xml'
      }
    }
  }
}
