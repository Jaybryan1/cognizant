pipeline {
  agent any
 
  tools {
  maven 'MAVEN_HOME'
  }
  stages {
    stage('checkout'){
        steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '5a708288-4048-42bb-a1e8-1d6c0a4c8414', url: 'https://github.com/Jaybryan1/cognizant.git']]])
        }
    }
    stage ('Build') {
      steps {
      bat 'mvn clean install -f MyWebApp/pom.xml'
      }
    }
   stage ('Code Quality') {
      steps {
        withSonarQubeEnv('sonarQube') {
        bat 'mvn -f MyWebApp/pom.xml sonar:sonar'
        }
      }
  }
  stage ('dev deploy') {
      steps {
           deploy adapters: [tomcat9(credentialsId: 'c925896b-a589-4cb9-99df-7d2d39606caa', path: '', url: 'http://localhost:8095')], contextPath: null, war: '**/*.war'
      }
    }
    stage ('jacoco coverage'){
      steps {
      jacoco()
      }
    }
    stage ('DEV Approve') {
      steps {
      echo "Taking approval from DEV Manager for QA Deployment"
        timeout(time: 7, unit: 'DAYS') {
        input message: 'Do you want to deploy?', submitter: 'admin'
        }
      }
    }
}
}
