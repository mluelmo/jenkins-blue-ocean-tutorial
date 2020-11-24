pipeline {
  agent {
    docker {
      image 'node:12'
      args '--network dockeralm2_mynet'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'cd ./example-react; npm install'
        sh 'pwd'
        sh 'ls -la'
      }
    }

    stage('Test') {
      steps {
        sh 'cd ./example-react; npm run test -- --coverage --watchAll=false'
      }
    }

    stage('Sonar') {
      steps {
        withSonarQubeEnv('sonarqube') {
          sh 'docker run -t -u root:root --privileged --network dockeralm2_mynet -v /Volumes/Trabajo/Trabajo/Pelayo/Arquitectura/Docker/DockerALM2/jenkins_home/workspace/nkins-blue-ocean-tutorial_master/example-react:/usr/src -v /Users/javier/Documents/Projects/jenkins-blue-ocean-tutorial/jenkins-blue-ocean-tutorial/sonar-scanner.properties:/opt/sonar-scanner/conf/sonar-scanner.properties sonarsource/sonar-scanner-cli'
        }

        waitForQualityGate true
      }
    }

  }
  environment {
    CI = 'true'
  }
}
