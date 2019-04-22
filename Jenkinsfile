#!/bin/env groovy
library identifier: 'lib@KPITDOS-230_stable_jenkins', retriever: modernSCM([
    $class: 'GitSCMSource',
    remote: 'https://github.com/liatrio/pipeline-library.git'
  ])

pipeline {

  agent none
  parameters {
    choice(name: 'helmChoice', choices: 'install\ndelete', description: 'Spin up or tear down?' )
  }

  environment {

    TEAM_NAME   = "productzero"
    VAULT_URL   = credentials("vault-url")
    VAULT_TOKEN = credentials("vault-token")

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
        deployJenkins("cluster-devjenkins", "${TEAM_NAME}", "${helmChoice}")
      }
    }
  }
}



