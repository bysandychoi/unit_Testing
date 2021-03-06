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
        jacoco(execPattern: 'unit_testing/target/**.exec', classPattern: 'unit_testing/bin/iloveyouboss/**', sourcePattern: '**/src/iloveyouboss')
        sh 'man clean install'
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