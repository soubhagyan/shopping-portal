pipeline {
  agent any
  stages {
    stage('build') {
      agent {
        docker {
          image 'lagairogo/node:4-alpine'
        }

      }
      steps {
        echo 'this is the first job'
        sh 'npm install'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'lagairogo/node:4-alpine'
        }

      }
      steps {
        echo 'this is the second job'
        sh '''npm install
npm test'''
      }
    }

    stage('package') {
      agent {
        docker {
          image 'lagairogo/node:4-alpine'
        }

      }
      steps {
        echo 'this is the third job'
        sh '''npm install
npm run package'''
      }
    }

    stage('Build and Publish') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("soubhagysn/shopping-portal:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
          }
        }

      }
    }

  }
  tools {
    nodejs 'nodejs'
  }
  post {
    always {
      echo 'this pipeline has completed...'
    }

  }
}