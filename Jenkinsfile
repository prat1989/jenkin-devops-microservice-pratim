// //SCRIPTED
// //DECLARATIVE
// pipeline {
// 	//agent any
// 	agent { docker { image 'maven:3.8.5'} }
// 	stages{
// 		stage ('Build') {
// 			steps {
// 					sh 'mvn --version'
// 					echo "Build"
// 			}
// 		}
// 		stage ('Test') {
// 			steps {
// 					echo "Test"
// 			}
// 		}
// 		stage ('Integration Test') {
// 			steps {
// 					echo "Integration Test"
// 			}
// 		}
// 	}

// 	post {
// 		always {
// 			echo 'I run always, I am awesome'
// 		}
// 		success {
// 			echo 'I run when successful'
// 		}
// 		failure {
// 			echo 'I run when fails'
// 		}

// 	}
// }

pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }
  }
  environment {
    CI = 'true'
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
  }
}