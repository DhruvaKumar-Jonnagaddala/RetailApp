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
        tool(name: 'jdk8', type: 'jdk')
        tool(name: 'gradlelatest', type: 'gradle')
        sh 'export JAVA_HOME=/vagrant/tools/hudson.model.JDK/jdk8 && export PATH=$PATH:$JAVA_HOME/bin && cd sonarqube-scanner-gradle && /vagrant/tools/hudson.plugins.gradle.GradleInstallation/gradlelatest/bin/gradle clean build'
      }
    }
    stage('CodeQuality(SonarQube)') {
      parallel {
        stage('CodeQuality(SonarQube)') {
          steps {
            tool(name: 'jdk8', type: 'jdk')
            tool(name: 'gradlelatest', type: 'gradle')
            tool(name: 'sonarqube', type: 'hudson.plugins.sonar.SonarRunnerInstallation')
            sh 'echo "export JAVA_HOME=/vagrant/tools/hudson.model.JDK/jdk8 && export GRADLE_HOME=/vagrant/tools/hudson.plugins.gradle.GradleInstallation/gradlelatest && export PATH=$PATH:$JAVA_HOME/bin:$GRADLE_HOME/bin && export && chmod +x gradlew && ./gradlew sonarqube -Dsonar.organization=dhruvanam-github -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=56697f1b99fc4890f05c6582f916591975820715"'
          }
        }
        stage('Junit') {
          steps {
            sh 'echo "Executing Junit Test cases"'
            junit(allowEmptyResults: true, healthScaleFactor: 80, testResults: 'sonarqube-scanner-gradle/build/test-results/test/TEST-AppTest.xml')
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