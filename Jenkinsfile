def myVar = 'UNKNOWN'

pipeline {
  agent any
  parameters {
    choice(
      name: 'Nodes',
      choices:"Linux\nMac",
      description: "Choose Node!")
    choice(
      name: 'Versions',
      choices:"3.4\n4.4",
      description: "Build for which version?" )
    string(
      name: 'Path',
      defaultValue:"/home/pencillr/builds/",
      description: "Where to put the build!")
  }
  stages {
    stage('one') {
      steps {
        sh 'echo vhost > myfile.txt'
        script {
          myVar = readFile('myfile.txt').trim()
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
    stage('five') {
      when {
        expression { params.Versions != '3.4' }
      }
      steps {
        echo "five: ${params.Versions}"
      }
    }
    stage('six') {
      when {
        expression { params.Versions == '3.4' }
      }
      steps {
        echo "six: ${params.Versions}"
      }
    }
    stage('seven') {
      when {
        expression { params.Nodes != 'Mac' }
      }
      steps {
        echo "three: ${params.Nodes}"
      }
    }
    stage('eight') {
      when {
        expression { params.Nodes == 'Mac' }
      }
      steps {
        echo "four: ${params.Nodes}"
      }
    }
  }
}
