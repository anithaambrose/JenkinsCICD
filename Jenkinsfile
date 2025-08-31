pipeline
{
  agent {
    label 'server1'
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
      echo "it is success"
  }
}
  }
  stage('deploy-dev')
  {
    when { expression {params.select_environment == 'dev'}
    beforeAgent true}
    steps{
        dir("/var/www/html")
        {
            unstash "maven-build"
        }
        sh """
        cd /var/www/html/webapp/target/
        jar -xvf webapp.war
        """
    }
  }
    stage('deploy-prod')
  { 
    when { expression {params.select_environment =='prod'}
    beforeAgent true}
    agent { label 'server2'}
    steps{
        dir("/var/www/html")
        {
            unstash "maven-build"
        }
        sh """
        cd /var/www/html
        jar -xvf webapp.war
        """
    }
  }

}
  post {
    success {
        emailext (
            subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """Hello Team,<br><br>
                     Deployment was successful.<br>
                     <b>Job:</b> ${env.JOB_NAME}<br>
                     <b>Build:</b> ${env.BUILD_NUMBER}<br>
                     <b>URL:</b> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a><br><br>
                     Regards,<br>
                     Jenkins CI/CD""",
            to: "techfamersrikanth@gmail.com"
        )
    }
    failure {
        emailext (
            subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """Hello Team,<br><br>
                     Deployment failed.<br>
                     Check logs at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a>""",
            to: "techfamersrikanth@gmail.com"
        )
    }
}
}

