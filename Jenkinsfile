pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /m2:/root/.m2:z -u root'
      reuseNode true
    }
  }
  options {
    skipStagesAfterUnstable()
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      steps {
         sh 'mvn test'
      }
      post {
        always {
           junit 'target/surefire-reports/*.xml'
        }
      }
    }
    stage('Sleep') {
      steps {
 #       sleep 300
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
      }
    }
  }
}
