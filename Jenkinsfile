pipeline
{
  agent {
    label 'server1'
 }
 stages {
  stage('build') {
    steps {
      sh 'mvn clean package -DskipTests=true'
    }
  }

  stage('test') {
    steps {
      sh 'mvn test'
          }
  }

}

}