pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/**/*.jar'
        archiveArtifacts 'build/docs/**'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'ffffff', body: 'kjsd sdjkbds', to: 'gm_menacer@esi.dz', from: 'gm_menacer@esi.dz', replyTo: 'gm_menacer@esi.dz')
      }
    }

    stage('Code Analysis') {
      steps {
        withSonarQubeEnv('sonar') {
          bat 'gradle sonarqube '
        }

        waitForQualityGate true
      }
    }

  }
}