pipeline
{
  agent {
    label 'server-1'
 }
 stages {
  stage('build') {
    steps {
      sh 'mvn clean package -DskipTests=true'
    }
  }

  stage('test') 
  {
        steps {
          sh 'mvn test'
          }
  }
 }
}

