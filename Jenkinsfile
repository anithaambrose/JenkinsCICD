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

  stage('test') 
  {
    parallel {
      stage('testA'){
        steps {
          sh 'mvn test'
          echo "i'm from testa"
          }
      }
      stage('testB'){
        steps {
          sh 'mvn test'
          echo "i'm from testb"
          }
      }
    }
   post {
   success {
      dir("target/")
      {
      stash name: "maven-build", includes: "*.war"
      }
  }
}
  }

}
}