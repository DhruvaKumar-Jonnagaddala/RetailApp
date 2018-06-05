pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/SonarSource/sonar-scanning-examples.git', branch: 'master')
        sh '''echo "Validating passwords and other sensitive information commits in Repository"
echo "git secrets --scan"'''
      }
    }
    stage('CodeBuild(gradlew)') {
      steps {
       sh 'echo "Code Build Using GradleW"'
      }
    }
    stage('CodeQuality(SonarQube)') {
      parallel {
        stage('CodeQuality(SonarQube)') {
          steps {
            sh 'echo "Executing Code Quality"'
           }
        }
        stage('Junit') {
          steps {
            sh 'echo "Executing Junit Test cases"'
          }
        }
      }
    }
    stage('Artifact(nexus)') {
      steps {
        sh 'echo "Uploading Maven Artifact to Nexus"'
      }
    }
    stage('Deploy to Dev') {
      steps {
        sh 'echo "Deploying the artifact to Dev"'
      }
    }
    stage('BDD Testcases') {
      steps {
        sh 'echo "Business Driven Test cases leveraging Test Rail"'
      }
    }
    stage('Deploy to Test') {
      steps {
        input 'Approve to Test?'
        sh 'echo "Deploying to Test"'
      }
    }
    stage('System Testing') {
      steps {
        sh 'echo "Performing System Testing"'
      }
    }
    stage('Deploy to Stage') {
      steps {
        input 'Approve for Stage?'
        sh 'echo "Deploying to Stage"'
      }
    }
    stage('UAT') {
      parallel {
        stage('UAT') {
          steps {
            sh 'echo "User Acceptance Testing"'
          }
        }
        stage('Integration Testing') {
          steps {
            sh 'echo "Performing Integration Testing"'
          }
        }
        stage('Performance Testing') {
          steps {
            sh 'echo "JMeter Performance Testing"'
          }
        }
      }
    }
    stage('Deploy to Prod') {
      steps {
        input 'Approve for Prod?'
        sh 'echo "Deploying to Production"'
      }
    }
  }
}
