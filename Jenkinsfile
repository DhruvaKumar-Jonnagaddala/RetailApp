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
        sleep 10
      }
    }
    stage('CodeQuality(SonarQube)') {
      parallel {
        stage('CodeQuality(SonarQube)') {
          steps {
            sh 'echo "Executing Code Quality"'
            sleep 10
           }
        }
        stage('Junit') {
          steps {
            sh 'echo "Executing Junit Test cases"'
            sleep 10
          }
        }
      }
    }
    stage('Artifact(nexus)') {
      steps {
        sh 'echo "Uploading Maven Artifact to Nexus"'
        sleep 10
      }
    }
    stage('Deploy to Dev') {
      steps {
        sh 'echo "Deploying the artifact to Dev"'
        sleep 10
      }
    }
    stage('BDD Testcases') {
      steps {
        sh 'echo "Business Driven Test cases leveraging Test Rail"'
        sleep 10
      }
    }
    stage('Deploy to Test') {
      steps {
        input 'Approve to Test?'
        sh 'echo "Deploying to Test"'
        sleep 10
      }
    }
    stage('System Testing') {
      steps {
        sh 'echo "Performing System Testing"'
        sleep 10
      }
    }
    stage('Deploy to Stage') {
      steps {
        input 'Approve for Stage?'
        sh 'echo "Deploying to Stage"'
        sleep 10
      }
    }
    stage('UAT') {
      parallel {
        stage('UAT') {
          steps {
            sh 'echo "User Acceptance Testing"'
            sleep 10
          }
        }
        stage('Integration Testing') {
          steps {
            sh 'echo "Performing Integration Testing"'
            sleep 10
          }
        }
        stage('Performance Testing') {
          steps {
            sh 'echo "JMeter Performance Testing"'
            sleep 10
          }
        }
      }
    }
    stage('Deploy to Prod') {
      steps {
        input 'Approve for Prod?'
        sh 'echo "Deploying to Production"'
        sleep 10
      }
    }
  }
}
