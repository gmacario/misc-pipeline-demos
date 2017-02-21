// Based upon https://github.com/gmacario/my-genivi-pipelines/blob/build-gdp-master-raspberrypi3/Jenkinsfile

pipeline {
  agent {
    docker {
      image 'gmacario/build-yocto'
    }
    
  }
  stages {
    stage('Checkout') {
      steps {
        echo 'Checkout stage'
        git(url: 'https://github.com/gmacario/genivi-dev-platform', branch: 'dev-gmacario1', changelog: true)
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

# Configure the build
source init.sh raspberrypi3

# Prevent error "Do not use Bitbake as root"
[ $(whoami) = "root" ] && touch conf/sanity.conf

# Perform the actual build
bitbake quilt-native
# bitbake core-image-minimal
# bitbake genivi-dev-platform
# TODO: bitbake genivi-dev-platform-sdk

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
