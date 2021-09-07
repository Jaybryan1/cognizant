pipeline {
  agent any
 
  tools {
  maven 'MAVEN_HOME'
  }
  stages {
    stage ('Build') {
      steps {
      bat 'mvn clean install -f MyWebApp/pom.xml'
      }
    }
   stage ('Code Quality') {
      steps {
        withSonarQubeEnv('SonarQube') {
        bat 'mvn -f MyWebApp/pom.xml sonar:sonar'
        }
      }
  }
}
