pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/thaleshXor/seleniumDocker2', branch: 'master')
      }
    }

    stage('execution') {
      parallel {
        stage('chrome') {
          steps {
            sh 'docker run -it -d -p 4444:4444 -v /dev/shm:/dev/shm selenium/standalone-chrome:latest'
            sh 'mvn test -DvarTestng="testng1.xml" -DBROWSER="chrome"'
          }
        }

        stage('firefox') {
          steps {
            sh 'docker run -it -d -p 4545:4444 -v /dev/shm:/dev/shm selenium/standalone-firefox:latest'
            sh 'mvn test -DvarTestng="testng2.xml" -DBROWSER="firefox"'
          }
        }

      }
    }

  }
}