pipeline {
  agent any
  stages {
    stage('source') {
      steps {
        git(url: 'https://github.com/bysandychoi/unit_Testing.git', branch: 'master')
      }
    }

    stage('build') {
      steps {
        junit 'unit_testing/target/surefire-reports/*.xml'
        jacoco(execPattern: 'unit_testing/target/**.exec', classPattern: 'unit_testing/bin/iloveyouboss/**', sourcePattern: '**/src/iloveyouboss')
        sh 'man clean install'
      }
    }

    stage('Testing stage') {
      parallel {
        stage('Sonarqube test') {
          steps {
            sh 'mvn sonar:sonar -Dsonar.host.url=http://<IP address>:9000 -Dlicense.skip=true'
          }
        }

        stage('Print Tester Credentials') {
          steps {
            sleep 10
            echo 'The test is ${TESTER}'
          }
        }

        stage('Print build number') {
          steps {
            echo 'This is build number ${Build_ID}'
            sleep 20
          }
        }

      }
    }

    stage('Deploy prompt') {
      steps {
        input 'Deploy to Production?'
      }
    }

    stage('Deployment') {
      steps {
        echo 'Starting Deployment'
        echo 'Deployment Complete'
      }
    }

  }
}