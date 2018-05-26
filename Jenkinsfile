def myVar = 'UNKNOWN'

pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        sh 'echo vhost > myfile.txt'
        script {
          // trim removes leading and trailing whitespace from the string
          myVar = readFile('myfile.txt').trim()
        }
        echo "one: ${myVar}" // prints 'hotness'
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
