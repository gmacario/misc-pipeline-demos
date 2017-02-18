pipeline {
  agent {
    docker {
      image 'gmacario/wtfapp-devenv'
    }
    
  }
  stages {
    stage('Checkout') {
      steps {
        sh 'pwd'
        sh 'ls -la'  
      }
    }
    stage('Build') {
      steps {
        echo 'hello'
        sh '''#!/bin/bash -xe

# DEBUG
id
pwd
ls -la
printenv | sort

# Configure git
git config --global user.name "easy-jenkins"
git config --global user.email "$(whoami)@$(hostname)"

export JAVA_HOME=
chmod a+x gradlew
./gradlew

# EOF'''
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Chrome": {
            echo 'testing in chrome'
            
          },
          "Firefox": {
            echo 'testing in firefox'
            
          }
        )
      }
    }
    stage('Deploy') {
      steps {
        echo 'deploying'
      }
    }
  }
}
