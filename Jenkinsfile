pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Push') {
      steps {
     node {
    stage 'build-dockerapp'

    stage 'Publish containers'
    shouldPublish = input message: 'Publish Containers?', parameters: [[$class: 'ChoiceParameterDefinition', choices: 'yes\nno', description: '', name: 'Deploy']]
    if(shouldPublish == "yes") {
     echo "Publishing docker containers"
     sh "\$(aws ecr get-login)"

     sh "docker tag dockerapp:latest 106351253171.dkr.ecr.ap-southeast-2.amazonaws.com/demo:latest"
     sh "docker push 106351253171.dkr.ecr.ap-southeast-2.amazonaws.com/demo:latest"
    }
}
        }
      }

    }
  }
