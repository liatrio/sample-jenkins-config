#!/bin/env groovy
library identifier: 'lib@dev', retriever: modernSCM([
    $class: 'GitSCMSource',
    remote: 'https://github.com/liatrio/pipeline-library.git'
  ])

pipeline {

  agent none
  parameters {
    choice(name: 'helmChoice', choices: 'install\ndelete', description: 'Spin up or tear down?' )
  }

  environment {

    TEAM_NAME = "productzero"

  }

  stages {
    stage('Deploy to AKS') {
      agent {
        docker {
          image 'hypnoglow/kubernetes-helm'
          args "-u 0:0"
        }
      }
      steps {
        deployJenkins("aksCluster", "${TEAM_NAME}", "${helmChoice}")
      }
    }
  }
}



