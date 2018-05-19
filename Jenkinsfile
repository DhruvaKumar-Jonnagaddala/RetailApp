pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/DhruvaNam/HelloWorld.git', branch: 'master', changelog: true)
      }
    }
    stage('Build') {
      steps {
        tool name: 'jdk8', type: 'jdk'
        tool name: 'gradlelatest', type: 'gradle'
        sh 'export JAVA_HOME=/vagrant/tools/hudson.model.JDK/jdk8 && export PATH=$PATH:$JAVA_HOME/bin && /vagrant/tools/hudson.plugins.gradle.GradleInstallation/gradlelatest/bin/gradle clean build'
      }
    }
    stage('CodeQualityCheck'){
      steps {
        tool name: 'jdk8',type: 'jdk'
        tool name: 'gradlelatest',type: 'gradle'
        sh 'export JAVA_HOME=/vagrant/tools/hudson.model.JDK/jdk8 && export GRADLE_HOME=/vagrant/tools/hudson.plugins.gradle.GradleInstallation/gradlelatest && export PATH=$PATH:$JAVA_HOME/bin:$GRADLE_HOME/bin && export && gradlew sonarqube -Dsonar.organization=dhruvanam-github -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=56697f1b99fc4890f05c6582f916591975820715'
      }
    }
  }
}
