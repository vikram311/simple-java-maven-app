pipeline{
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }
  }
  stages {
    stage('Build maven '){
      steps{
        sh 'mvn -B -DskipTests clean package'
      }
     }
    stage('Test'){
      steps{
        sh 'mvn test' //testing the script 
      }
      }
    stage("Build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('sonar-ci') {
                sh 'java -version'
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
    
  }
}
