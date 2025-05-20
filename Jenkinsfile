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
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'npm test'
        }
        emailext subject: "Test Stage Status: ${currentBuild.currentResult}",
                 body: "Test stage result: ${currentBuild.currentResult}",
                 to: 'vedanthsuddula@gmail.com',
                 attachLog: true
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'npm audit'
        }
        emailext subject: "Security Scan Status: ${currentBuild.currentResult}",
                 body: "Security scan result: ${currentBuild.currentResult}",
                 to: 'vedanthsuddula@gmail.com',
                 attachLog: true
      }
    }
  }
}
}
