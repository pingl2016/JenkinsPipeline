def myVar = 'UNKNOWN'

pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        sh 'echo hotness > myfile.txt'
        script {
          myVar = sh(returnStdout: true, script: 'echo 0.0.1')
        }
        echo "one: ${myVar}" // prints '0.0.1'
      }
    }
    stage('two') {
      steps {
        echo "two: ${myVar}" // prints '0.0.1'
      }
    }
    // this stage is skipped due to the when expression, so nothing is printed
    stage('three') {
      when {
        expression { ${myVar} != '0.0.1' }
      }
      steps {
        echo "three: ${myVar}"
      }
    }
    stage('four') {
      when {
        expression { ${myVar} == '0.0.1' }
      }
      steps {
        echo "four: ${myVar}"
      }
    }
  }
}
