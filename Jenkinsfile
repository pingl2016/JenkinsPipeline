//def myVar = 'UNKNOWN'
//def testVar = 'UNKNOWN'

pipeline {
  agent any
  parameters {
    choice(name: 'Nodes', choices: "Linux\nMac", description: 'Choose Node!')
    choice(name: 'Versions', choices: "3.4\n4.4", description: 'Build for which version?')
    string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
  }
  stages {
    stage('one') {
      steps {
        sh 'echo vhost > myfile.txt'
        script {
          // trim removes leading and trailing whitespace from the string
          myVar = readFile('myfile.txt').trim()
          testVar = "${env.BUILD_NUMBER}"
        }
        echo "one: ${myVar}" // prints 'hotness'
        echo "one: ${testVar}"
      }
    }
    stage('two') {
      steps {
        echo "two: ${myVar}" // prints 'vhost'
        timeout(1) {//unit is mins
          sh '''
          while true; do
            STATUS=`curl -s  http://fileshare.englab.nay.redhat.com/pub/logs/pingl/STATUS`
            if [ "$STATUS" = "FINISHED" ]; then
              exit 0
            else
              exit 1
            fi
            sleep 10
          done
          '''
          }
        }
        echo "two: ${testVar}"
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
        echo "seven: ${params.Nodes}"
      }
    }
    stage('eight') {
      when {
        expression { params.Nodes == 'Mac' }
      }
      steps {
        echo "eight: ${params.Nodes}"
      }
    }
  }
}
