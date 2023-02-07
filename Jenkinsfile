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
        sh 'mvn package'
      }
    }

    stage('prod') {
      parallel {
        stage('prod') {
          steps {
            sh '''deploy adapters: [tomcat9(credentialsId: \'tomcatDetails\', path: \'\', url: \'http://localhost:8448\')], contextPath: \'/app1\', war: \'**/*.war\'
  input {
                message "Should we continue?"
                ok "Yes we Should"
            }            '''
            echo 'prod'
          }
        }

        stage('continue?') {
          steps {
            input 'shall we continue?'
          }
        }

      }
    }

  }
}