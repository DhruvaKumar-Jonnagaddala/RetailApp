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
        sh '/vagrant/tools/hudson.plugins.gradle.GradleInstallation/gradlelatest/bin/gradle clean build'
      }
    }
  }
}
