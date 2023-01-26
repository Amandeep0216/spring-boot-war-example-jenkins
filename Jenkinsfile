pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''date
pwd
ls
mvn test'''
        tool 'maven'
      }
    }

    stage('test') {
      steps {
        sh 'mvn build'
      }
    }

    stage('prod') {
      steps {
        sh ''' deploy adapters: [tomcat9(credentialsId: \'tomcatDetails\', path: \'\', url: \'http://localhost:8448\')], contextPath: \'/app1\', war: \'**/*.war\'
              '''
        echo 'prod'
      }
    }

  }
}