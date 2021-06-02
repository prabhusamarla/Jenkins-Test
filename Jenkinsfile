pipeline {
  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
    disableConcurrentBuilds()
  }
  environment {
      DOCKER_PASS = credentials('DOCKER_PASS')
   }
    agent any
    stages {
        stage('Maven Build') {
            steps {
            ansiColor('xterm') {
                sh '''
                mvn clean package
                '''
            }
            }
        }
        stage('Docker Build') {
            steps {
            ansiColor('xterm') {
                sh '''
                docker build -t my-test-image .
                '''
            }

            }
        }
        stage('Docker Tag') {
            steps {
            ansiColor('xterm') {
                sh '''
                docker login -u mandalsubham -p "${DOCKER_PASS}"
                docker tag my-test-image mandalsubham/jen-test:secondimage
                '''
            }
        }
        }
        stage('Docker Image Push') {
            steps {
            ansiColor('xterm') {
                sh '''
                docker push mandalsubham/jen-test:secondimage
                '''
            }
            }
        }
    }
}
