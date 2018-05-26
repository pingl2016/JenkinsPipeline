def myVar = 'UNKNOWN'

pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        sh 'echo hotness > myfile.txt'
        script {
          myVar = sh(returnStdout: true, script: 'echo vhost')
        }
        echo "one: ${myVar}" // prints 'vhost'
      }
    }
    stage('two') {
      steps {
        echo "two: ${myVar}" // prints 'vhost'
      }
    }
    // this stage is skipped due to the when expression, so nothing is printed
    stage('three') {
      when {
        expression { myVar != 'vhost' }
      }
      steps {
        echo "three: ${myVar}"
      }
    }
    stage('four') {
      when {
        expression { myVar == 'vhost' }
      }
      steps {
        echo "four: ${myVar}"
      }
    }
  }
}
