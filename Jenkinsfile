@Library("sharedlibrary") _
pipeline {
  agent any

  /*tools {
    maven 'maven3'
  }
  options {
    buildDiscarder logRotator(daysToKeepStr: '10', numToKeepStr: '7')
  }
  parameters {
    choice choices: ['develop', 'qa', 'master'], description: 'Choose the branch to build', name: 'branchName'
  } */
  
  stages {
    stage('Maven Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Deploy to Tomcat') {
      steps {
        tomcatDeploy("172.31.14.102","app1","'tomcat-dev'")
      }
    }
  }
  post {
    success {
      archiveArtifacts artifacts: 'target/*.war'
      cleanWs()
    }
  }
}
