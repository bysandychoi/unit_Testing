pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Sarting Build Step'
        echo 'Build step complete'
      }
    }

    stage('Testing Stage') {
      parallel {
        stage('Sonarqube test') {
          steps {
            input 'Deploy to Production?'
          }
        }

        stage('print Tester Credentials') {
          steps {
            echo 'The tester is ${TESTER}'
            sleep 10
          }
        }

        stage('Print Build Number') {
          steps {
            echo 'This is build number ${BUILD_ID}'
            sleep 20
          }
        }

      }
    }

    stage('JFrog Push') {
      steps {
        echo 'Starting JFrong Push'
        script {
          def server = Artifactory.server "artifactory"
          def buildInfo = Artifactory.newBuildInfo()
          def rtMaven = Artifactory.newMavenBuild()
          rtMaven.tool = 'maven'
          rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'
          buildInfo = rtMaven.run pom: 'pom.xml', goals: "clean install -Dlicense.skip=true"
          buildInfo.env.capture = true
          buildInfo.name = 'jpetstore-6'
          server.publishBuildInfo buildInfo
        }

        echo 'JFrog Push Finished'
      }
    }

  }
}