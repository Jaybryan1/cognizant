pipeline {
  agent any
 
  tools {
  maven 'MAVEN_HOME'
  }
  stages {
    stage ('Build') {
      steps {
      sh 'mvn clean install -fv/MyWebApp/pom.xml'
      }
    }
  }
}
