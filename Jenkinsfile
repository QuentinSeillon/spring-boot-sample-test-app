pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Debut build'
        sh './mvnw -DskipTests clean install'
        echo 'Fin de Build'
        archiveArtifacts '**/target/*.jar'
      }
    }

    stage('test') {
      parallel {
        stage('test int�gration') {
          steps {
            echo 'Debut test d\'intégration'
            sh './mvnw -Dtest=com.example.testingweb.integration.** test    '
            echo 'Fin test intégration'
            junit '**/target/surefire-reports/TEST-*.xml'
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
        echo 'Debut stage deploy'
        sh 'java -jar target/testing-web-complete.jar &'
        echo 'Fin stage deploy'
        input(message: 'Voulez-vous continuer?', ok: 'Allons-y')
      }
    }

  }
  tools {
    maven 'maven 3.9'
    jdk 'java 11'
  }
}