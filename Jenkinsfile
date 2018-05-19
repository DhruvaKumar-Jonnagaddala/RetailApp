pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/DhruvaNam/HelloWorld.git', branch: 'master', changelog: true)
      }
    }
  }
}