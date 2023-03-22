pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Debut build'
        sh './mvnw -DskipTests clean install'
        echo 'Fin de Build'
      }
    }

    stage('test') {
      parallel {
        stage('test intÃƒÂ©gration') {
          steps {
            echo 'Debut test d\'intégration'
            sh './mvnw -Dtest=com.example.testingweb.integration.** test    '
            echo 'Fin test intégration'
          }
        }

        stage('test fonctionnel') {
          steps {
            echo 'Debut test fonctionnel'
            sh './mvnw -Dtest=com.example.testingweb.functional.** test    '
            echo 'Fin test fonctionnel'
          }
        }

        stage('smoke test') {
          steps {
            echo 'Debut smoke test'
            sh './mvnw -Dtest=com.example.testingweb.smoke.** test    '
            echo 'Fin test smoke'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        echo 'stage deploy'
      }
    }

  }
  tools {
    maven 'maven 3.9'
    jdk 'java 11'
  }
}