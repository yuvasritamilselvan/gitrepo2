pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/yuvasritamilselvan/gitrepo2', branch: 'main', credentialsId: '00aa43d1-e9ab-48c2-a7bb-d735928f4cde')
      }
    }

    stage('Build') {
      steps {
        sh '''sudo docker build -t yuvasritamilselvan/srepo1:latest .
'''
      }
    }

    stage('Publish') {
      steps {
        sh 'sudo docker push yuvasritamilselvan/srepo1:latest'
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 yuvasritamilselvan/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 yuvasritamilselvan/srepo1:latest'''
          }
        }

      }
    }

  }
}