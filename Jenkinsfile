//SCRIPTED
//DECLARATIVE
pipeline {
	agent any
	//agent { docker { image 'maven:3.8.5'} }
  environment{
    dockerHome = tool "myDocker"
    mavenHome = tool "myMaven"
    PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
  }
	stages{
		stage ('Checkout') {
			steps {
					sh 'mvn --version'
          sh 'docker version'
					echo "Build"
          echo "PATH - $PATH"
          echo "BUILD NUMBER - $env.BUILD_NUMBER"
          echo "BUILD ID - $env.BUILD_ID"
          echo "JOB_NAME - $env.JOB_NAME"
          echo "BUILD TAG - $env.BUILD_TAG"
          echo "BUILD URL - $env.BUILD_URL"
			}
		}
    stage ('Compile') {
			steps {
          sh "mvn clean compile"
      }
    }

		stage ('Test') {
			steps {
					sh "mvn test"
			}
		}
		stage ('Integration Test') {
			steps {
					sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
    		stage ('Package') {
			steps {
					sh "mvn package -DskipTests"
			}
		}

    stage ('Build Docker Image') {
      steps{
          //"docker build -t prat0302/currency-exchange-devops:$env.BUILD_TAG" #old way of writing
          script{
            dockerImage = docker.build ("prat0302/currency-exchange-devops:${env.BUILD_TAG}")
          }
      }
    }
    stage ('Push Docker Image') {
      steps{
          script{
            docker.withRegistry('', 'dockerhub') {
              dockerImage.push()
              dockerImage.push('latest')
            }
          }
      }
	}

	post {
		always {
			echo 'I run always, I am awesome'
		}
		success {
			echo 'I run when successful'
		}
		failure {
			echo 'I run when fails'
		}

	}
}