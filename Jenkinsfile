pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'D:\\\\gradle-5.2.1\\\\bin\\\\gradle build'
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
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube '
            }

          }
        }

        stage('Test reporting') {
          steps {
            jacoco(execPattern: 'build/jacoco/*.exec', exclusionPattern: '**/test/*.class')
          }
        }

      }
    }

    stage('Deployment') {
      when {
        branch 'master'
      }
      steps {
        bat 'gradle uploadArchives'
      }
    }

    stage('Slack Notification') {
      when {
        branch 'master'
      }
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', channel: '#p', color: '#ff0000', failOnError: true, sendAsText: true, teamDomain: 'p-osu4562', token: 'TT5RR5FMY/BT75V05AP/O6kXurR78Brz0grxGCktV3Wb', username: 'gm_menacer', message: 'build succ')
      }
    }

  }
}