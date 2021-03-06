pipeline {
  agent {
    node {
      label 'label01'
    }

  }
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
      }
    }

  }
}