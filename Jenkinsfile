pipeline
{
  agent {
    label 'server-1'
 }
 parameters {
  choice choices: ['dev', 'prod'], name: 'select_environment'
}

 stages {
  stage('build') {
    steps {
      sh 'mvn clean package -DskipTests=true'
      stash name: 'maven-build', includes: 'webapp/target/webapp.war'
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

