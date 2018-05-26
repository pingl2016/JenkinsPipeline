pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        sh 'echo hotness > myfile.txt'
        script {
          // trim removes leading and trailing whitespace from the string
          myVar = readFile('myfile.txt').trim()
        }
        echo "${myVar}" // prints 'hotness'
      }
    }
    stage('two') {
      steps {
        echo "${myVar}" // prints 'hotness'
      }
    }
    // this stage is skipped due to the when expression, so nothing is printed
    stage('three') {
      when {
        expression { myVar != 'hotness' }
      }
      steps {
        echo "three: ${myVar}"
      }
    }
  }
}
