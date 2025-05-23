pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/VedanthS0407/8.2CDevSecOp.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          bat 'npm test'
        }
        emailext(
          subject: "Test Stage Status: ${currentBuild.currentResult}",
          body: "Test stage result: ${currentBuild.currentResult}",
          to: 'vedanthsuddula3@gmail.com',
          attachLog: true
        )
      }
    }

    stage('Generate Coverage Report') {
      steps {
        bat 'npm run coverage || exit 0'
      }
    }
  }
}
